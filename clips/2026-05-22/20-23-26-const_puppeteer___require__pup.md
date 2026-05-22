---
date: 2026-05-22T20:23:26+08:00
source: clipboard
chars: 1273
---

const puppeteer = require('puppeteer-core');
const fs = require('fs-extra');
const path = require('path');

// 你的摹客链接
const URL = 'https://app.mockplus.cn/app/share-77968423f1e7976fc5c4c676155d43dcshare-4Vg8MNEC3/design';

// 自动用你本地的 Edge 浏览器
const EDGE = '/Applications/Microsoft Edge.app/Contents/MacOS/Microsoft Edge';

(async () => {
  const browser = await puppeteer.launch({
    executablePath: EDGE,
    headless: false,
    args: ['--no-sandbox']
  });

  const page = await browser.newPage();
  await page.goto(URL, { waitUntil: 'networkidle2' });
  await page.waitForSelector('.list-item');

  // 获取所有页面
  const items = await page.$$('.list-item');
  console.log('✅ 总页数：', items.length);

  // 创建输出文件夹
  await fs.ensureDir('./pages');

  // 自动翻页 + 自动截图
  for (let i = 0; i < items.length; i++) {
    console.log('正在导出第', i+1, '页');

    await items[i].click();
    await new Promise(r => setTimeout(r, 1000));

    // 截图画板
    const canvas = await page.$('canvas');
    await canvas.screenshot({
      path: `./pages/page_${i+1}.png`,
      type: 'png'
    });
  }

  console.log('🎉 全部导出完成！文件夹：pages/');
  await browser.close();
})();
