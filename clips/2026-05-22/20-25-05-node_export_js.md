---
date: 2026-05-22T20:25:05+08:00
source: clipboard
chars: 1978
---

 node export.js
file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer-core/lib/puppeteer/common/QueryHandler.js:211
                const waitForSelectorError = new (error instanceof TimeoutError ? TimeoutError : Error)(`Waiting for selector \`${selector}\` failed`);
                                             ^

TimeoutError: Waiting for selector `.list-item` failed
    at CSSQueryHandler.waitFor (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer-core/lib/puppeteer/common/QueryHandler.js:211:46)
    at async CdpFrame.waitForSelector (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer-core/lib/puppeteer/api/Frame.js:541:21)
    at async CdpPage.waitForSelector (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer-core/lib/puppeteer/api/Page.js:1387:20)
    at async /Users/zhengzixuan/Downloads/fenbi-helper-master/export.js:20:3 {
  cause: TimeoutError: Waiting failed: 30000ms exceeded
      at new WaitTask (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer-core/lib/puppeteer/common/WaitTask.js:46:34)
      at IsolatedWorld.waitForFunction (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer-core/lib/puppeteer/api/Realm.js:49:26)
      at CSSQueryHandler.waitFor (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer-core/lib/puppeteer/common/QueryHandler.js:176:95)
      at async CdpFrame.waitForSelector (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer-core/lib/puppeteer/api/Frame.js:541:21)
      at async CdpPage.waitForSelector (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer-core/lib/puppeteer/api/Page.js:1387:20)
      at async /Users/zhengzixuan/Downloads/fenbi-helper-master/export.js:20:3
}

Node.js v25.8.2
zhengzixuan@MCdeMBP fenbi-helper-master % 
zhengzixuan@MCdeMBP fenbi-helper-master % 

