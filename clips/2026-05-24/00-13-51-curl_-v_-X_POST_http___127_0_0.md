---
date: 2026-05-24T00:13:51+08:00
source: clipboard
chars: 189
---

curl -v -X POST http://127.0.0.1:3456/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "lite",
    "messages": [{"role": "user", "content": "你好"}]
  }'
