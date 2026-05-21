---
date: 2026-05-22T00:26:20+08:00
source: clipboard
chars: 156
---

const allAreas = [...new Set(
    suites.map(s => getAreaTag(s.name))
        .filter(tag => tag && !/^\d{4}$/.test(tag)) // 过滤掉纯年份的标签
)];
