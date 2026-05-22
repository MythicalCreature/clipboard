---
date: 2026-05-22T21:12:37+08:00
source: clipboard
chars: 162
---

mkdir -p mockplus_origin && cat links.txt | xargs -n 1 curl -H "Referer: https://app.mockplus.cn/" -H "User-Agent: Mozilla/5.0" -O -# --output-dir mockplus_origin
