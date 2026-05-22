---
date: 2026-05-22T20:41:22+08:00
source: clipboard
chars: 175
---

performance.getEntriesByType('resource')
  .map(i => i.name)
  .filter(u => u.includes('.png') && !u.includes('thumb') && u.startsWith('http'))
  .forEach(u => console.log(u))
