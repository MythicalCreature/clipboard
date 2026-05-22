---
date: 2026-05-22T23:15:30+08:00
source: clipboard
chars: 250
---

curl http://localhost:4000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "spark-lite",
    "messages": [
      {"role": "user", "content": "帮我分析一道公考行测言语理解题，讲解技巧"}
    ]
  }'
