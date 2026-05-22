---
date: 2026-05-22T21:08:06+08:00
source: clipboard
chars: 699
---

// ==UserScript==
// @name         摹客提取原图链接
// @namespace    http://tampermonkey.net/
// @version      1.0
// @match        *://app.mockplus.cn/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    setTimeout(()=>{
        const urls = new Set();
        performance.getEntriesByType('resource').forEach(res=>{
            let u = res.name;
            if(u.includes('.png') && !u.includes('thumb') && !u.includes('webp')){
                urls.add(u);
            }
        });
        const res = Array.from(urls).join('\n');
        console.log('纯净原图链接:\n',res);
        alert('链接已输出到控制台，复制即可');
    },3000);
})();
