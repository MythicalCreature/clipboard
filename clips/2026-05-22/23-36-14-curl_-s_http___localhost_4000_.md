---
date: 2026-05-22T23:36:14+08:00
source: clipboard
chars: 300
---

curl -s http://localhost:4000/v1/chat/completions \
-H "Content-Type: application/json" \
-d '{"model":"lite","messages":[{"role":"user","content":"广东公考申论行政执法卷怎么拿高分"}]}' \
| python3 -c "import sys, json; print(json.load(sys.stdin)['choices'][0]['message']['content'])"
