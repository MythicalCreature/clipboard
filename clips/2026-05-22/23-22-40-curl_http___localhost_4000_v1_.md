---
date: 2026-05-22T23:22:40+08:00
source: clipboard
chars: 238
---

curl http://localhost:4000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "spark-lite",
    "messages": [
      {"role": "user", "content": "广东公考申论行政执法卷怎么写高分"}
    ]
  }'
