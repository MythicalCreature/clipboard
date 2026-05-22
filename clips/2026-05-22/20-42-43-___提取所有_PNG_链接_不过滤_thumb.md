---
date: 2026-05-22T20:42:43+08:00
source: clipboard
chars: 182
---

// 提取所有 PNG 链接，不过滤 thumb
performance.getEntriesByType('resource')
  .map(req => req.name)
  .filter(url => /\.png/.test(url))
  .forEach(url => console.log(url));
