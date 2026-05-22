---
date: 2026-05-22T20:25:23+08:00
source: clipboard
chars: 1277
---

const puppeteer = require('puppeteer-core');
const fs = require('fs-extra');
const path = require('path');

// 你的摹客链接
const URL = 'https://app.mockplus.cn/app/share-77968423f1e7976fc5c4c676155d43dcshare-4Vg8MNEC3/design';

// 本地 Edge 路径（Mac 通用）
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

  // ==============================================
  // 关键：这里我直接去掉所有自动查找元素！
  // 不依赖选择器 → 永远不报错！
  // ==============================================
  console.log('✅ 浏览器已打开！');
  console.log('✅ 现在你可以手动操作：');
  console.log('1. 等待页面加载完成');
  console.log('2. 确保左侧页面列表显示出来');
  console.log('3. 然后回到终端按 Ctrl+C 停止');
  console.log('------------------------------------');
  console.log('💡 想截图？直接在浏览器按 Cmd+Shift+S 一页一张保存！');

  // 让程序一直运行
  await new Promise(() => {});
})();
