---
date: 2026-05-21T21:18:46+08:00
source: clipboard
chars: 3272
---

const fs = require('fs');
const path = require('path');

// 主函数：p标签自动换行 + 保留下划线/书名号/标点
async function createJson() {
    console.log("⏳ 第一步：获取收藏题目ID...");
    const ids = await getQuestionIds();
    console.log("✅ 获取到题目ID：", ids.length + " 题");

    console.log("⏳ 第二步：获取题目详情...");
    const rawData = await getQuestionDetail(ids);
    console.log("✅ 题目详情获取完成，开始生成 JSON...");

    const ansArr = ["A", "B", "C", "D", "E", "F"];
    const questions = [];
    const index = 27;
    const name = "2023广东言语理解与表达"; // 你的文件名
    const fileName = name + ".json";

    for (let i = 0; i < rawData.solutions.length; i++) {
        const q = rawData.solutions[i];
        const num = i + 1;

        const stem = parseHtmlWithParagraphs(q.content);

        const options = [];
        if (Number(q.type) === 5) {
            options.push("正确");
            options.push("错误");
        } else {
            for (const opt of q.accessories[0].options) {
                const txt = parseHtmlWithParagraphs(opt);
                options.push(txt);
            }
        }

        let answer = "";
        if (q.type === 2) {
            answer = formatMultiAnswer(q.correctAnswer.choice);
        } else if (q.type === 5) {
            answer = q.correctAnswer.choice === "0" ? "A" : "B";
        } else {
            answer = ansArr[Number(q.correctAnswer.choice)] || "";
        }

        const analysis = parseHtmlWithParagraphs(q.solution);
        const sourceLink = await getSourceLinkHtml(q.solution, q.content);
        const fullAnalysis = analysis + sourceLink;

        questions.push({
            id: `s${index}q${num}`,
            suiteIndex: index,
            suiteName: name,
            num: num,
            type: "选择题",
            stem: stem,
            options: options,
            answer: answer,
            analysis: fullAnalysis
        });
    }

    const output = {
        name: name,
        count: questions.length,
        questions: questions
    };

    // 1. 生成你的题库 JSON
    fs.writeFileSync(fileName, JSON.stringify(output, null, 4), "utf8");

    // 2. 👇👇👇 自动维护 files.json（核心！）
    updateFilesJson(fileName);

    console.log("🎉 JSON 导出完成！");
    console.log("✅ files.json 已自动更新！");
}

// =============================================
// 👇 这就是自动维护 files.json 的函数
// =============================================
function updateFilesJson(newFileName) {
    const filesJsonPath = path.join(__dirname, "files.json");
    let fileList = [];

    // 如果 files.json 已存在，读取现有内容
    if (fs.existsSync(filesJsonPath)) {
        const content = fs.readFileSync(filesJsonPath, "utf8");
        try {
            fileList = JSON.parse(content);
        } catch (e) {
            fileList = [];
        }
    }

    // 如果文件名不在列表里，才添加（避免重复）
    if (!fileList.includes(newFileName)) {
        fileList.push(newFileName);
    }

    // 写回 files.json
    fs.writeFileSync(filesJsonPath, JSON.stringify(fileList, null, 2), "utf8");
}
