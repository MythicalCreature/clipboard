---
date: 2026-05-22T20:33:50+08:00
source: clipboard
chars: 1253
---

const puppeteer = require('puppeteer-core');
const fs = require('fs-extra');
const path = require('path');

const URL = 'https://app.mockplus.cn/app/share-77968423f1e7976fc5c4c676155d43dcshare-4Vg8MNEC3/design';
const EDGE = '/Applications/Microsoft Edge.app/Contents/MacOS/Microsoft Edge';
const SAVE_DIR = './mock_img';
const MAX_COUNT = 50;
// 单张截取尺寸
const W = 380, H = 820;
// 行列排布
const col = 2;
const gap = 30;

(async () => {
  await fs.ensureDir(SAVE_DIR);
  const browser = await puppeteer.launch({
    executablePath: EDGE,
    headless: false,
    args: ['--no-sandbox']
  });
  const page = await browser.newPage();
  await page.goto(URL);
  await new Promise(r => setTimeout(r, 6000));

  for(let i = 0; i < MAX_COUNT; i++){
    const c = i % col;
    const r = Math.floor(i / col);
    const x = c * (W + gap);
    const y = r * (H + gap);

    await page.evaluate((sx,sy)=>window.scrollTo(sx-50, sy-50),x,y);
    await new Promise(r=>setTimeout(r,800));

    const file = path.join(SAVE_DIR, `img_${i+1}.png`);
    await page.screenshot({
      path: file,
      clip:{x,y,width:W,height:H}
    });
    console.log(`已保存第${i+1}张`);
  }

  await browser.close();
  console.log('全部50张截取完毕');
})();
