---
date: 2026-05-24T00:28:55+08:00
source: clipboard
chars: 188
---

curl -X POST http://127.0.0.1:3456/任意路径都可以 \
  -H "Content-Type: application/json" \
  -d '{
    "model": "lite",
    "messages": [{"role": "user", "content": "你好"}]
  }'
