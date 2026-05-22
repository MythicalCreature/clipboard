---
date: 2026-05-22T20:27:20+08:00
source: clipboard
chars: 3227
---

const puppeteer = require('puppeteer-core');
const fs = require('fs-extra');
const path = require('path');

// -------------------------- 配置区（不用改，直接用）--------------------------
const MOCKPLUS_URL = 'https://app.mockplus.cn/app/share-77968423f1e7976fc5c4c676155d43dcshare-4Vg8MNEC3/design';
const OUTPUT_DIR = './mockplus-auto-exports';
const EDGE_PATH = '/Applications/Microsoft Edge.app/Contents/MacOS/Microsoft Edge';
// -----------------------------------------------------------------------------

(async () => {
  console.log('🚀 正在启动自动导出工具...');
  
  // 1. 初始化浏览器（使用你本地的Edge，跳过下载）
  const browser = await puppeteer.launch({
    executablePath: EDGE_PATH,
    headless: false, // 保留窗口，方便你看进度
    args: [
      '--no-sandbox',
      '--disable-setuid-sandbox',
      '--start-maximized',
      '--disable-blink-features=AutomationControlled'
    ]
  });

  const page = await browser.newPage();
  await page.setViewport({width: 1920, height: 1080, deviceScaleFactor: 2}); // 2倍高清截图

  // 2. 打开摹客页面
  console.log('🌐 正在加载摹客页面...');
  await page.goto(MOCKPLUS_URL, { waitUntil: 'networkidle2', timeout: 60000 });
  await new Promise(r => setTimeout(r, 3000)); // 额外等待页面渲染

  // 3. 自动识别所有页面（适配摹客的真实DOM结构）
  console.log('🔍 正在识别所有页面...');
  const pageItems = await page.$$eval('[role="treeitem"]', items => 
    items.filter(el => el.querySelector('[class*="title"]') || el.textContent.trim())
  );
  const pageList = await page.$$('[role="treeitem"]');
  console.log(`✅ 共识别到 ${pageList.length} 个页面`);

  if (pageList.length === 0) {
    console.error('❌ 未找到页面列表，请检查页面是否加载完成');
    await browser.close();
    return;
  }

  // 4. 创建输出文件夹
  await fs.ensureDir(OUTPUT_DIR);

  // 5. 循环自动导出每一页
  for (let i = 0; i < pageList.length; i++) {
    console.log(`\n📄 正在导出第 ${i+1}/${pageList.length} 页`);

    // 切换到当前页面
    await pageList[i].click();
    await new Promise(r => setTimeout(r, 2500)); // 等待页面切换+渲染

    // 获取页面名称（用于文件名）
    const pageName = await page.evaluate(() => {
      const activeItem = document.querySelector('[role="treeitem"][aria-selected="true"]');
      return activeItem?.querySelector('[class*="title"]')?.textContent.trim() || `page_${String(i+1).padStart(3, '0')}`;
    });

    // 截图当前画板（适配摹客的Canvas渲染）
    const canvas = await page.$('canvas[class*="artboard"], .artboard-container canvas');
    if (!canvas) {
      console.warn(`⚠️ 未找到画板，跳过：${pageName}`);
      continue;
    }

    // 保存为PNG
    const filename = path.join(OUTPUT_DIR, `${pageName}.png`);
    await canvas.screenshot({
      path: filename,
      type: 'png',
      omitBackground: true
    });

    console.log(`✅ 已保存：${filename}`);
  }

  // 6. 导出完成
  console.log(`\n🎉 所有页面导出完成！文件保存在：${path.resolve(OUTPUT_DIR)}`);
  await browser.close();
})();
