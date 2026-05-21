---
date: 2026-05-22T00:20:03+08:00
source: clipboard
chars: 201
---

 const allProvinces = [...new Set(suites.map(s => {
                const match = s.name.match(/(^|[^\d])([^0-9\s]+)/);
                return match ? match[2] : null;
            }).filter(Boolean))];
