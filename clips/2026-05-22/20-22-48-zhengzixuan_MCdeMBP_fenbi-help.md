---
date: 2026-05-22T20:22:48+08:00
source: clipboard
chars: 2528
---

zhengzixuan@MCdeMBP fenbi-helper-master % npm install puppeteer fs-extra  
npm error code 1
npm error path /Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer
npm error command failed
npm error command sh -c node install.mjs
npm error **INFO** Skipping Firefox download as instructed.
npm error Error: ERROR: Failed to set up chrome-headless-shell v148.0.7778.167! Set "PUPPETEER_SKIP_DOWNLOAD" env variable to skip download.
npm error     at downloadBrowser (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer/lib/puppeteer/node/install.js:26:15)
npm error     at async Promise.all (index 1)
npm error     at async downloadBrowsers (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer/lib/puppeteer/node/install.js:84:9) {
npm error   [cause]: Error: All providers failed for chrome-headless-shell 148.0.7778.167:
npm error     - DefaultProvider: Extraction failed:   End-of-central-directory signature not found.  Either this file is not
npm error     a zipfile, or it constitutes one disk of a multi-part archive.  In the
npm error     latter case the central directory and zipfile comment will be found on
npm error     the last disk(s) of this archive.
npm error   unzip:  cannot find zipfile directory in one of /Users/zhengzixuan/.cache/puppeteer/chrome-headless-shell/148.0.7778.167-chrome-headless-shell-mac-arm64.zip or
npm error           /Users/zhengzixuan/.cache/puppeteer/chrome-headless-shell/148.0.7778.167-chrome-headless-shell-mac-arm64.zip.zip, and cannot find /Users/zhengzixuan/.cache/puppeteer/chrome-headless-shell/148.0.7778.167-chrome-headless-shell-mac-arm64.zip.ZIP, period.
npm error   
npm error       at installWithProviders (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/@puppeteer/browsers/lib/install.js:107:11)
npm error       at async install (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/@puppeteer/browsers/lib/install.js:117:12)
npm error       at async downloadBrowser (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer/lib/puppeteer/node/install.js:14:24)
npm error       at async Promise.all (index 1)
npm error       at async downloadBrowsers (file:///Users/zhengzixuan/Downloads/fenbi-helper-master/node_modules/puppeteer/lib/puppeteer/node/install.js:84:9)
npm error }
npm error A complete log of this run can be found in: /Users/zhengzixuan/.npm/_logs/2026-05-22T12_22_38_089Z-debug-0.log
zhengzixuan@MCdeMBP fenbi-helper-master % 

