---
date: 2026-05-22T15:14:40+08:00
source: clipboard
chars: 28101
---

const fs = require('fs');
const axios = require('axios');
const sharp = require('sharp');
const path = require('path');
const { Document, Packer, Paragraph, TextRun, ImageRun, ExternalHyperlink, HyperlinkType } = require("docx");

// 题型映射
function getTypeText(type) {
    switch (Number(type)) {
        case 1: return "单选题";
        case 2: return "多选题";
        case 5: return "判断题";
        default: return "其他题型";
    }
}

// 多选答案格式化（修复双顿号）
function formatMultiAnswer(choiceStr) {
    const map = ["A", "B", "C", "D", "E", "F"];
    const validChars = choiceStr.replace(/[^0-5]/g, '').split('');
    return validChars.map(i => map[Number(i)]).join('、');
}

// 下划线处理
function cleanUnderlineSpaces(html) {
    if (!html) return "";
    return html.replace(/<u>\s*(&nbsp;|\s)*<\/u>/g, '__UNDERLINE__');
}

// 题干专用：按 p 标签分段，自动换行，保留段落结构
function parseHtmlPartsForQuestion(html) {
    const parts = [];
    html = cleanUnderlineSpaces(html);

    // 核心：按 p 标签分割，实现自动分段
    const pSegments = html.split(/<\/p>/i);

    for (let seg of pSegments) {
        if (!seg.trim()) continue;

        // 清理剩余标签
        seg = seg.replace(/<p\s*\/?>/gi, "").trim();
        if (!seg) continue;

        const reg = /(<img[^>]+>)|(__UNDERLINE__)/g;
        const split = seg.split(reg);

        for (let s of split) {
            if (!s || s.trim() === '') continue;
            if (s.startsWith("<img")) {
                const src = s.match(/src="([^"]+)"/)[1];
                const isTex = /flag\s*=\s*["']tex["']/i.test(s);
                parts.push({ type: "image", url: src, isTex });
            } else if (s === "__UNDERLINE__") {
                parts.push({ type: "underline" });
            } else {
                const text = s.replace(/<[^>]+>/g, "").trim();
                if (text) parts.push({ type: "text", value: text });
            }
        }

        // 每个 p 标签结束，加一个分段标记
        parts.push({ type: "paragraphBreak" });
    }

    return parts;
}

// 加载图片并读取元数据（修复无协议URL）
async function loadImagesAndMeta(parts) {
    for (const p of parts) {
        if (p.type === "image") {
            try {
                let url = p.url;
                if (url.startsWith("//")) {
                    url = "https:" + url;
                }
                const res = await axios.get(url, { responseType: "arraybuffer" });
                p.buffer = Buffer.from(res.data);
                const meta = await sharp(p.buffer).metadata();
                p.width = meta.width;
                p.height = meta.height;
            } catch (e) {
                console.error("❌ 图片加载失败：", p.url, e.message);
                p.buffer = null;
            }
        }
    }
}

// 统一缩放图片（支持题干/解析/选项三种尺寸）
function resizeImage(p, isForSolution = false, isOptionImg = false) {
    if (!p.buffer || !p.width || !p.height) return;
    if (p.isTex) {
        p.width = 50;
        p.height = Math.round(p.height * 30 / p.width);
    } else {
        let targetWidth = 300;
        if (isForSolution) targetWidth = 200;
        if (isOptionImg) targetWidth = 120;
        const scale = targetWidth / p.width;
        p.width = targetWidth;
        p.height = Math.round(p.height * scale);
    }
}

// 构建题干段落（带题型前缀）
// 构建题干段落（带题型前缀 + 按 p 标签分段换行）
function buildPara(parts, prefixText = "") {
    const children = [];
    let runs = [];

    if (prefixText) {
        runs.push(new TextRun({ text: prefixText, size: 24 }));
    }

    for (const p of parts) {
        if (p.type === "text") {
            runs.push(new TextRun({ text: p.value + " ", size: 24 }));
        }
        if (p.type === "underline") {
            runs.push(new TextRun({
                text: "        ", size: 24,
                underline: { type: "single", color: "000000" }
            }));
        }
        if (p.type === "image" && p.buffer) {
            if (p.isTex) {
                runs.push(new ImageRun({
                    data: p.buffer,
                    transformation: { width: p.width, height: p.height },
                    verticalAlignment: "baseline"
                }));
                runs.push(new TextRun({ text: " " }));
            } else {
                if (runs.length > 0) {
                    children.push(new Paragraph({ children: runs }));
                    runs = [];
                }
                children.push(new Paragraph({
                    alignment: "center",
                    children: [new ImageRun({
                        data: p.buffer,
                        transformation: { width: p.width, height: p.height }
                    })]
                }));
            }
        }
        // 遇到段落分隔，立即换行
        if (p.type === "paragraphBreak") {
            if (runs.length > 0) {
                children.push(new Paragraph({ children: runs }));
                runs = [];
            }
        }
    }

    if (runs.length > 0) {
        children.push(new Paragraph({ children: runs }));
    }

    const fixedParas = [];
    for (let i = 0; i < children.length; i++) {
        const para = children[i];
        fixedParas.push(para);
        const curr = para.childElements?.[0];
        const next = children[i + 1]?.childElements?.[0];
        const isText = curr && !curr.imageData;
        const nextIsImage = next && next.imageData;
        if (isText && !nextIsImage) {
            fixedParas.push(new Paragraph(""));
        }
    }

    return fixedParas;
}

// 解析专用：保留p标签的HTML解析
function parseHtmlParts(html) {
    const parts = [];
    html = cleanUnderlineSpaces(html);
    const reg = /(<img[^>]+>)|(__UNDERLINE__)/g;
    const split = html.split(reg);

    for (let s of split) {
        if (!s || s.trim() === '') continue;
        if (s.startsWith("<img")) {
            const src = s.match(/src="([^"]+)"/)[1];
            const isTex = /flag\s*=\s*["']tex["']/i.test(s);
            parts.push({ type: "image", url: src, isTex });
        } else if (s === "__UNDERLINE__") {
            parts.push({ type: "underline" });
        } else {
            parts.push({ type: "text", value: s });
        }
    }
    return parts;
}

// 构建解析段落（p标签自动换行 + 完整保留原文内容 + 解码HTML实体）
function buildSolutionPara(parts) {
    const paras = [];
    let runs = [];

    function flush() {
        if (runs.length > 0) {
            paras.push(new Paragraph({ children: [...runs] }));
            runs = [];
        }
    }

    function decodeHtmlEntities(str) {
        return str
            .replace(/&lt;/g, "<")
            .replace(/&gt;/g, ">")
            .replace(/&amp;/g, "&")
            .replace(/&quot;/g, '"')
            .replace(/&apos;/g, "'");
    }

    for (const part of parts) {
        if (part.type === "text") {
            let html = part.value || "";
            html = html.replace(/<p\s*\/?>/gi, "\n").replace(/<\/p>/gi, "\n");
            const lines = html.split(/\n/);

            for (let line of lines) {
                line = line.replace(/<[^>]+>/g, "").trim();
                line = decodeHtmlEntities(line);

                if (!line) {
                    flush();
                } else {
                    runs.push(new TextRun({ text: line + " ", size: 24 }));
                }
            }
        } else if (part.type === "image" && part.buffer) {
            flush();
            if (part.isTex) {
                runs.push(
                    new ImageRun({
                        data: part.buffer,
                        transformation: { width: part.width, height: part.height },
                        verticalAlignment: "baseline"
                    })
                );
                runs.push(new TextRun({ text: " ", size: 24 }));
            } else {
                paras.push(
                    new Paragraph({
                        alignment: "center",
                        children: [
                            new ImageRun({
                                data: part.buffer,
                                transformation: { width: part.width, height: part.height },
                            }),
                        ],
                    })
                );
            }
        }
    }
    flush();
    return paras;
}

// 选项专用：解析选项文本中的图片和文字
function parseOptionText(text) {
    const runs = [];
    const reg = /(<img[^>]+>)/g;
    const parts = text.split(reg);

    for (const part of parts) {
        if (!part.trim()) continue;
        if (part.startsWith("<img")) {
            const src = part.match(/src="([^"]+)"/)[1];
            const isTex = /flag\s*=\s*["']tex["']/i.test(part);
            runs.push({ type: "image", url: src, isTex });
        } else {
            const cleanText = part.replace(/<[^>]+>/g, "").trim();
            if (cleanText) {
                runs.push({ type: "text", value: cleanText });
            }
        }
    }
    return runs;
}

// 获取收藏题目ID
async function getQuestionIds() {
    try {
        const res = await axios({
            url: "https://tiku.fenbi.com/api/xingce/questionIds?type=collects&categoryId=21016&offset=0&limit=420&order=desc&timeRange=0&app=web&kav=125&av=127&hav=125&version=3.0.0.0&deviceId=&gav=2&apcId=0",
            headers: {
                "accept": "application/json, text/plain, */*",
                "cookie": "sajssdk_2015_cross_new_user=1; device_id=v1_31r8qf3bfeorc_c6f7; sid=3496335; persistent=P/9KU4ejTjN95KWdULv4DQdfObS+qUw016k8+Qm7nHWRgnppl7zHPNov/BSEnYsTZfQ2W2JFTxvlzYNBOdtcrA==; sensorsdata2015jssdkcross=%7B%22distinct_id%22%3A%22153862080%22%2C%22first_id%22%3A%2219e4e704ffd913-09dd83f7da5ae18-7e433c49-1484784-19e4e704ffe26bd%22%2C%22props%22%3A%7B%22%24latest_traffic_source_type%22%3A%22%E7%9B%B4%E6%8E%A5%E6%B5%81%E9%87%8F%22%2C%22%24latest_search_keyword%22%3A%22%E6%9C%AA%E5%8F%96%E5%88%B0%E5%80%BC_%E7%9B%B4%E6%8E%A5%E6%89%93%E5%BC%80%22%2C%22%24latest_referrer%22%3A%22%22%7D%2C%22identities%22%3A%22eyIkaWRlbnRpdHlfY29va2llX2lkIjoiMTllNGU3MDRmZmQ5MTMtMDlkZDgzZjdkYTVhZTE4LTdlNDMzYzQ5LTE0ODQ3ODQtMTllNGU3MDRmZmUyNmJkIiwiJGlkZW50aXR5X2xvZ2luX2lkIjoiMTUzODYyMDgwIn0%3D%22%2C%22history_login_id%22%3A%7B%22name%22%3A%22%24identity_login_id%22%2C%22value%22%3A%22153862080%22%7D%2C%22%24device_id%22%3A%2219e4e704ffd913-09dd83f7da5ae18-7e433c49-1484784-19e4e704ffe26bd%22%7D; acw_tc=276a356617794327822745832efb6910b89681ee460e79c2021efa7d0abda5; Hm_lvt_e7351028cde0d0ccb9ccdbe5fe531683=1779432444,1779432706,1779433024,1779433249; Hm_lpvt_e7351028cde0d0ccb9ccdbe5fe531683=1779433249; HMACCOUNT=162EE110FE0CBBBA; userid=153862080; sess=sEPVn/i1/aOgW1SO6plNfGF2yhMm4RBKuSBAYlrXFprgmgxUfZpzOyC1WUPbihrFDv8Wuoh3BvJg/miqW//nOmLbbboKHcBIjVB7w60VwqI=",
                "Referer": "https://www.fenbi.com/",
            },
            method: "GET"
        });
        console.log(res.data);
        return res.data.results;
    } catch (err) {
        console.error('❌ 获取题目ID失败');
        return [];
    }
}

// 获取题目详情（自动切块，每次300个ID，防止接口报错）
async function getQuestionDetail(ids) {
    try {
        const allSolutions = [];
        const chunkSize = 300; // 每次最多请求300题

        // 把 ids 切成每300个一组
        for (let i = 0; i < ids.length; i += chunkSize) {
            const chunkIds = ids.slice(i, i + chunkSize);
            const idStr = chunkIds.join(',');

            console.log(`⏳ 正在请求题目：第 ${i + 1} ~ ${Math.min(i + chunkSize, ids.length)} 题`);

            const res = await axios({
                method: "GET",
                url: `https://tiku.fenbi.com/api/xingce/universal/auth/solutions?type=2&questionIds=${idStr}&app=web&kav=125&av=127&hav=125&version=3.0.0.0&deviceId=&gav=2&apcId=0`,
                headers: {
                    "accept": "application/json, text/plain, */*",
                    "cookie": "sajssdk_2015_cross_new_user=1; device_id=v1_31r8qf3bfeorc_c6f7; sid=3496335; persistent=P/9KU4ejTjN95KWdULv4DQdfObS+qUw016k8+Qm7nHWRgnppl7zHPNov/BSEnYsTZfQ2W2JFTxvlzYNBOdtcrA==; sensorsdata2015jssdkcross=%7B%22distinct_id%22%3A%22153862080%22%2C%22first_id%22%3A%2219e4e704ffd913-09dd83f7da5ae18-7e433c49-1484784-19e4e704ffe26bd%22%2C%22props%22%3A%7B%22%24latest_traffic_source_type%22%3A%22%E7%9B%B4%E6%8E%A5%E6%B5%81%E9%87%8F%22%2C%22%24latest_search_keyword%22%3A%22%E6%9C%AA%E5%8F%96%E5%88%B0%E5%80%BC_%E7%9B%B4%E6%8E%A5%E6%89%93%E5%BC%80%22%2C%22%24latest_referrer%22%3A%22%22%7D%2C%22identities%22%3A%22eyIkaWRlbnRpdHlfY29va2llX2lkIjoiMTllNGU3MDRmZmQ5MTMtMDlkZDgzZjdkYTVhZTE4LTdlNDMzYzQ5LTE0ODQ3ODQtMTllNGU3MDRmZmUyNmJkIiwiJGlkZW50aXR5X2xvZ2luX2lkIjoiMTUzODYyMDgwIn0%3D%22%2C%22history_login_id%22%3A%7B%22name%22%3A%22%24identity_login_id%22%2C%22value%22%3A%22153862080%22%7D%2C%22%24device_id%22%3A%2219e4e704ffd913-09dd83f7da5ae18-7e433c49-1484784-19e4e704ffe26bd%22%7D; Hm_lvt_e7351028cde0d0ccb9ccdbe5fe531683=1779432444,1779432706,1779433024,1779433249; Hm_lpvt_e7351028cde0d0ccb9ccdbe5fe531683=1779433249; HMACCOUNT=162EE110FE0CBBBA; userid=153862080; sess=sEPVn/i1/aOgW1SO6plNfGF2yhMm4RBKuSBAYlrXFprgmgxUfZpzOyC1WUPbihrFDv8Wuoh3BvJg/miqW//nOmLbbboKHcBIjVB7w60VwqI=",
                    "Referer": "https://www.fenbi.com/",
                },
            });

            // 把当前块的题目加入总列表
            if (res.data?.solutions) {
                allSolutions.push(...res.data.solutions);
            }

            // 每块请求完延迟 300ms，避免请求太快被封
            await new Promise(r => setTimeout(r, 300));
        }

        console.log(`✅ 所有题目请求完成，共 ${allSolutions.length} 题`);
        return { solutions: allSolutions };

    } catch (err) {
        console.error('❌ 获取题目详情失败', err.message);
        return { solutions: [] };
    }
}

// ==============================================================================================
// 👇👇👇 核心匹配逻辑：提取 题干所有 p 标签内容 → 文章任意 p 标签完全一样 就匹配成功
// ==============================================================================================
function extractPureParagraphs(html) {
    if (!html) return [];
    const text = html.replace(/<[^>]+>/g, '').replace(/\s+/g, ' ').trim();
    return text ? [text] : [];
}

function isAnyParagraphExactMatch(questionHtml, articleContent) {
    const qParagraphs = extractPureParagraphs(questionHtml);
    const aParagraphs = extractPureParagraphs(articleContent);

    for (const qp of qParagraphs) {
        for (const ap of aParagraphs) {
            if (qp === ap) return true;
        }
    }
    return false;
}

function cleanText(text) {
    return text || '';
}

function getPureText(text) {
    if (!text) return "";
    const bookMatch = text.match(/《([^》]+)》/);
    let core = bookMatch ? bookMatch[1] : text;
    return core.replace(/[^\p{L}\p{N}]/gu, "").trim();
}

async function searchPeopleCN(keyword) {
    try {
        const res = await fetch("http://search.people.cn/search-platform/front/search", {
            headers: {
                "accept": "*/*",
                "content-type": "application/json",
                "cookie": "__jsluid_h=65a3a6dfad834f4ce8720e2128131b1f"
            },
            body: JSON.stringify({
                key: keyword, page: 1, limit: 10, hasTitle: true,
                hasContent: true, isFuzzy: true, type: 0, sortType: 2
            }),
            method: "POST"
        });
        return await res.json();
    } catch (e) { return null; }
}
// 清理标题：去掉 人民日报、《》、空格 等干扰字符
function cleanTitleForMatch(str) {
    if (!str) return "";
    return str
        .replace(/人民日报/g, "")       // 去掉“人民日报”
        .replace(/[《》【】\s]/g, "")   // 去掉书名号、空格
        .trim();
}

// 先标题模糊匹配 → 直接通过；否则再校验段落
function getBestTitleAndUrl(records, sourceKeyword, questionContent) {
    if (!records?.length) return null;

    // 先把出处清理干净
    const cleanSource = cleanTitleForMatch(sourceKeyword);

    // 1️⃣ 先遍历标题：清理后 包含 即算匹配
    for (const item of records) {
        const pureTitle = (item.title || "").replace(/<\/?em>/gi, "").trim();
        const cleanItemTitle = cleanTitleForMatch(pureTitle);

        // 核心：只要互相包含 → 直接成功
        const isMatch =
            cleanItemTitle.includes(cleanSource) ||
            cleanSource.includes(cleanItemTitle);

        if (isMatch) {
            console.log(pureTitle);
            return {
                title: pureTitle,
                url: item.originUrl || item.url || ""
            };
        }
    }

    // 2️⃣ 标题没匹配 → 再校验 p 标签内容
    const targetPure = getPureText(sourceKeyword);
    let best = null, maxScore = 0;

    for (const item of records) {
        const articleTxt = item.content || item.contentOriginal || "";
        if (!isAnyParagraphExactMatch(questionContent, articleTxt)) continue;

        const pureTitle = (item.title || "").replace(/<\/?em>/gi, "").trim();
        const currPure = getPureText(pureTitle);
        let score = 0;
        if (currPure === targetPure) score = 999;
        else if (currPure.includes(targetPure) || targetPure.includes(currPure)) score = 500;

        if (score > maxScore) {
            maxScore = score;
            best = { title: pureTitle, url: item.originUrl || item.url || "" };
        }
    }
    return best;
}
async function getSourceLinkPara(solutionText, questionContent) {
    if (!solutionText || !questionContent) return null;
    const match = solutionText.match(/【文段出处】(.+)/);
    if (!match) return null;

    let keyword = match[1].trim()
        .replace(/<[^>]+>/g, "")
        .replace(/&lt;/g, "<")
        .replace(/&gt;/g, ">")
        .replace(/&amp;/g, "&")
        .replace(/&quot;/g, '"')
        .replace(/&apos;/g, "'");

    const res = await searchPeopleCN(keyword);
    const best = getBestTitleAndUrl(res?.data?.records, keyword, questionContent);
    if (!best?.url) return null;

    return new Paragraph({
        children: [
            new TextRun({ text: "原文链接：", size: 24 }),
            new ExternalHyperlink({
                type: HyperlinkType.URL,
                link: best.url,
                children: [
                    new TextRun({
                        text: best.title,
                        size: 24, color: "0000FF", underline: true
                    })
                ]
            })
        ]
    });
}

// // 主函数
async function createDoc() {
    console.log("⏳ 第一步：获取收藏题目ID...");
    const ids = await getQuestionIds();
    console.log("✅ 获取到题目ID：", ids.length + " 题");

    console.log("⏳ 第二步：获取题目详情...");
    const rawData = await getQuestionDetail(ids);
    console.log("✅ 题目详情获取完成，开始生成Word...");

    const ansArr = ["A", "B", "C", "D"];
    const children = [];

    for (let i = 0; i < rawData.solutions.length; i++) {
        const q = rawData.solutions[i];
        const num = i + 1;

        children.push(new Paragraph({
            children: [new TextRun({ text: `第${num}题`, bold: true, size: 28 })]
        }));

        const tParts = parseHtmlPartsForQuestion(q.content);
        await loadImagesAndMeta(tParts);
        tParts.forEach(p => resizeImage(p, false));
        const typeName = getTypeText(q.type);
        const prefix = `【${typeName}】${num}. `;
        children.push(...buildPara(tParts, prefix));

        if (Number(q.type) === 5) {
            children.push(new Paragraph({ children: [new TextRun({ text: "A. 正确", size: 24 })] }));
            children.push(new Paragraph({ children: [new TextRun({ text: "B. 错误", size: 24 })] }));
        } else {
            for (let j = 0; j < q.accessories[0].options.length; j++) {
                const opt = q.accessories[0].options[j];
                const ans = ansArr[j];
                const optParts = parseOptionText(opt);
                await loadImagesAndMeta(optParts);
                optParts.forEach(p => resizeImage(p, false, true));

                const runs = [new TextRun({ text: `${ans}. `, size: 24 })];
                for (const part of optParts) {
                    if (part.type === "text") {
                        runs.push(new TextRun({ text: part.value + " ", size: 24 }));
                    } else if (part.type === "image" && part.buffer) {
                        runs.push(new ImageRun({
                            data: part.buffer,
                            transformation: { width: part.width, height: part.height },
                            verticalAlignment: "baseline"
                        }));
                    }
                }
                children.push(new Paragraph({ children: runs }));
            }
        }

        let answerText;
        if (q.type === 2) answerText = `答案：${formatMultiAnswer(q.correctAnswer.choice)}`;
        else answerText = `答案：${ansArr[Number(q.correctAnswer.choice)]}`;
        children.push(new Paragraph({
            children: [new TextRun({ text: answerText, bold: true, size: 24 })]
        }));

        children.push(new Paragraph({ children: [new TextRun({ text: "解析：", size: 24 })] }));
        const sParts = parseHtmlParts(q.solution);
        await loadImagesAndMeta(sParts);
        sParts.forEach(p => resizeImage(p, true));
        children.push(...buildSolutionPara(sParts));

        // ✅ 传入题干，按 p 标签完全匹配校验
        const linkPara = await getSourceLinkPara(q.solution, q.content);
        if (linkPara) children.push(linkPara);

        children.push(new Paragraph(""));
    }

    const doc = new Document({
        sections: [{ children }],
        styles: {
            paragraphStyles: [{
                id: "Normal",
                runProperties: { font: "宋体", size: 24, color: "000000" }
            }]
        }
    });

    const buffer = await Packer.toBuffer(doc);
    fs.writeFileSync("逻辑判断.docx", buffer);
    console.log("🎉 导出完成：逻辑判断.docx");
}

createDoc();

// 仅把 <u> 下划线转为 ________
function cleanUnderlineSpaces(html) {
    if (!html) return "";
    return html.replace(/<u\s*>(?:&nbsp;|\s)*<\/u>/gi, '________');
}

// 按 p 标签分段 + 按 br 换行 + 只清理 HTML 标签 + 保留所有符号
function parseHtmlWithParagraphs(html) {
    if (!html) return "";

    // 1. 先处理下划线
    html = cleanUnderlineSpaces(html);

    // 2. 把 <br> <br/> <br /> 全部换成换行符
    html = html.replace(/<br\s*\/?>/gi, '\n');

    // 3. 按 </p> 分割成段落
    const paragraphs = html.split(/<\/p>/i).map(p => {
        return p.replace(/<p\s*\/?>/gi, "")    // 去掉 <p>
            .replace(/<[^>]+>/g, "")       // 去掉所有其他标签
            .replace(/&nbsp;/g, " ")       // 空格转普通空格
            .replace(/[ \t]+/g, " ")       // 多个空格/制表符变一个
            .trim();
    }).filter(line => line); // 过滤空行

    // 4. 段落之间用换行连接（保留 br 产生的换行）
    return paragraphs.join('\n');
}

// ✅ 核心：获取【可点击链接文本】，直接加到解析里
// ✅ 生成网页可点击的 a 标签链接（核心！）
async function getSourceLinkHtml(solutionText, questionContent) {
    if (!solutionText || !questionContent) return "";
    const match = solutionText.match(/【文段出处】(.+)/);
    if (!match) return "";

    let keyword = match[1].trim()
        .replace(/<[^>]+>/g, "")
        .replace(/&lt;/g, "<")
        .replace(/&gt;/g, ">")
        .replace(/&amp;/g, "&")
        .replace(/&quot;/g, '"')
        .replace(/&apos;/g, "'");

    const res = await searchPeopleCN(keyword);
    const best = getBestTitleAndUrl(res?.data?.records, keyword, questionContent);
    if (!best?.url) return "";

    // 返回 网页可点击链接（关键！）
    return `\n原文链接：<a href="${best.url}" target="_blank" style="color:#0066cc; text-decoration:underline;">${best.title}</a>`;
}

// 主函数：p标签自动换行 + 保留下划线/书名号/标点
// async function createJson() {
//     console.log("⏳ 第一步：获取收藏题目ID...");
//     const ids = await getQuestionIds();
//     console.log("✅ 获取到题目ID：", ids.length + " 题");

//     console.log("⏳ 第二步：获取题目详情...");
//     const rawData = await getQuestionDetail(ids);
//     console.log("✅ 题目详情获取完成，开始生成 JSON...");

//     const ansArr = ["A", "B", "C", "D", "E", "F"];
//     const questions = [];
//     const index = 38;
//     const name = "2019广东选调言语理解与表达"; // 你的文件名
//     const fileName = name + ".json";

//     for (let i = 0; i < rawData.solutions.length; i++) {
//         const q = rawData.solutions[i];
//         const num = i + 1;

//         const stem = parseHtmlWithParagraphs(q.content);

//         const options = [];
//         if (Number(q.type) === 5) {
//             options.push("正确");
//             options.push("错误");
//         } else {
//             for (const opt of q.accessories[0].options) {
//                 const txt = parseHtmlWithParagraphs(opt);
//                 options.push(txt);
//             }
//         }

//         let answer = "";
//         if (q.type === 2) {
//             answer = formatMultiAnswer(q.correctAnswer.choice);
//         } else if (q.type === 5) {
//             answer = q.correctAnswer.choice === "0" ? "A" : "B";
//         } else {
//             answer = ansArr[Number(q.correctAnswer.choice)] || "";
//         }

//         const analysis = parseHtmlWithParagraphs(q.solution);
//         const sourceLink = await getSourceLinkHtml(q.solution, q.content);
//         const fullAnalysis = analysis + sourceLink;

//         questions.push({
//             id: `s${index}q${num}`,
//             suiteIndex: index,
//             suiteName: name,
//             num: num,
//             type: "选择题",
//             stem: stem,
//             options: options,
//             answer: answer,
//             analysis: fullAnalysis
//         });
//     }

//     const output = {
//         name: name,
//         count: questions.length,
//         questions: questions
//     };

//     // 1. 生成你的题库 JSON
//     fs.writeFileSync(fileName, JSON.stringify(output, null, 4), "utf8");

//     // 2. 👇👇👇 自动维护 files.json（核心！）
//     updateFilesJson(fileName);

//     console.log("🎉 JSON 导出完成！");
//     console.log("✅ files.json 已自动更新！");
// }

// =============================================
// 👇 这就是自动维护 files.json 的函数
// =============================================
// function updateFilesJson(newFileName) {
//     const filesJsonPath = path.join(__dirname, "files.json");
//     let fileList = [];

//     // 如果 files.json 已存在，读取现有内容
//     if (fs.existsSync(filesJsonPath)) {
//         const content = fs.readFileSync(filesJsonPath, "utf8");
//         try {
//             fileList = JSON.parse(content);
//         } catch (e) {
//             fileList = [];
//         }
//     }

//     // 如果文件名不在列表里，才添加（避免重复）
//     if (!fileList.includes(newFileName)) {
//         fileList.push(newFileName);
//     }

//     // 写回 files.json
//     fs.writeFileSync(filesJsonPath, JSON.stringify(fileList, null, 2), "utf8");
// }

// createJson();
