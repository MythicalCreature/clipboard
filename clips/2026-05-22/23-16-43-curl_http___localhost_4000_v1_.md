---
date: 2026-05-22T23:16:43+08:00
source: clipboard
chars: 217
---

curl http://localhost:4000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "spark-lite",
    "messages": [
      {"role": "user", "content": "公考申论怎么写高分"}
    ]
  }'
