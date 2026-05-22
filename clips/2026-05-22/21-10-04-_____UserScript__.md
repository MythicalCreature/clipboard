---
date: 2026-05-22T21:10:04+08:00
source: clipboard
chars: 1128
---

// ==UserScript==
// @name         摹客提取原图链接（全量版）
// @namespace    http://tampermonkey.net/
// @version      1.1
// @match        *://app.mockplus.cn/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    // 先滚动到页面最底部，让所有图片加载出来
    window.scrollTo(0, document.body.scrollHeight);
    setTimeout(() => {
        window.scrollTo(0, 0);
    }, 1000);

    // 延长等待到10秒，确保所有资源加载完成
    setTimeout(()=>{
        const urls = new Set();
        performance.getEntriesByType('resource').forEach(res=>{
            let u = res.name;
            // 过滤所有png，同时排除缩略图参数
            if(u.includes('.png') && !u.includes('thumb') && !u.includes('webp') && !u.includes('thumbnail')){
                urls.add(u);
            }
        });
        const res = Array.from(urls).join('\n');
        console.log('纯净原图链接:\n',res);
        alert(`已抓到 ${urls.size} 张原图链接，复制控制台内容即可`);
    }, 10000); // 改成10秒，不够的话可以再改到15000
})();
