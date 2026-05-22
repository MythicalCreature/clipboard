---
date: 2026-05-22T20:28:04+08:00
source: clipboard
chars: 1336
---

const puppeteer = require('puppeteer-core');
const fs = require('fs-extra');
const path = require('path');

const URL = 'https://app.mockplus.cn/app/share-77968423f1e7976fc5c4c676155d43dcshare-4Vg8MNEC3/design';
const EDGE = '/Applications/Microsoft Edge.app/Contents/MacOS/Microsoft Edge';

(async () => {
  console.log('✅ 启动 Edge...');

  const browser = await puppeteer.launch({
    executablePath: EDGE,
    headless: false,
    args: ['--no-sandbox']
  });

  const page = await browser.newPage();
  await page.goto(URL);
  await new Promise(r => setTimeout(r, 5000)); // 等页面完全加载

  console.log('✅ 开始自动翻页 + 自动截图');
  await fs.ensureDir('./pages');

  // ===========================
  // 摹客分享页专用 → 自动翻页
  // ===========================
  for (let i = 0; i < 999; i++) {
    try {
      // 截图当前页面
      const canvas = await page.$('canvas');
      await canvas.screenshot({
        path: `./pages/page_${i+1}.png`,
        type: 'png'
      });
      console.log('✅ 已保存第', i+1, '页');

      // 按下箭头 → 翻下一页
      await page.keyboard.press('ArrowDown');
      await new Promise(r => setTimeout(r, 1200));

    } catch (e) {
      console.log('🎉 全部导出完成！');
      break;
    }
  }

  await browser.close();
})();
