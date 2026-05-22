---
date: 2026-05-22T20:20:38+08:00
source: clipboard
chars: 2183
---

const puppeteer = require('puppeteer');
const fs = require('fs-extra');
const path = require('path');

// 配置：你的摹客分享链接
const MOCKPLUS_URL = 'https://app.mockplus.cn/app/share-77968423f1e7976fc5c4c676155d43dcshare-4Vg8MNEC3/design';
const OUTPUT_DIR = './mockplus-exports';

async function main() {
    // 创建输出目录
    await fs.ensureDir(OUTPUT_DIR);

    // 启动无头浏览器
    const browser = await puppeteer.launch({
        headless: false, // 可设为true后台运行
        args: ['--no-sandbox', '--disable-setuid-sandbox']
    });
    const page = await browser.newPage();
    await page.setViewport({width: 1920, height: 1080, deviceScaleFactor: 2}); // 2倍高清

    // 打开摹客页面
    await page.goto(MOCKPLUS_URL, {waitUntil: 'networkidle2'});
    await page.waitForSelector('[class*="page-item"], [class*="artboard-item"]', {timeout: 10000});

    // 获取所有页面
    const pages = await page.$$('[class*="page-item"], [class*="artboard-item"]');
    console.log(`找到 ${pages.length} 个页面`);

    // 循环导出每个页面
    for (let i = 0; i < pages.length; i++) {
        const pageEl = pages[i];
        const pageName = await page.evaluate(el => el.textContent.trim() || `page_${String(i+1).padStart(3, '0')}`, pageEl);
        const filename = path.join(OUTPUT_DIR, `mockplus_${pageName}.png`);

        console.log(`正在导出: ${pageName}`);

        // 点击切换页面
        await pageEl.click();
        await page.waitForTimeout(1500); // 等待加载

        // 等待画布渲染完成
        const canvasSelector = '[class*="artboard"], canvas[class*="artboard"]';
        await page.waitForSelector(canvasSelector, {timeout: 5000});

        // 截图当前画布
        const canvas = await page.$(canvasSelector);
        await canvas.screenshot({
            path: filename,
            type: 'png',
            omitBackground: true
        });

        console.log(`✅ 已保存: ${filename}`);
    }

    await browser.close();
    console.log('🎉 所有页面导出完成！');
}

main().catch(err => {
    console.error('❌ 导出失败:', err);
    process.exit(1);
});
