---
date: 2026-05-22T23:35:44+08:00
source: clipboard
chars: 267
---

curl -s http://localhost:4000/v1/chat/completions \
-H "Content-Type: application/json" \
-d '{"model":"lite","messages":[{"role":"user","content":"广东公考申论行政执法卷怎么拿高分"}]}' \
| python3 -m json.tool | grep -o '"content":.*' | cut -d'"' -f4
