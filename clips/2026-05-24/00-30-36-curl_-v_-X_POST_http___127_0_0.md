---
date: 2026-05-24T00:30:36+08:00
source: clipboard
chars: 158
---

curl -v -X POST http://127.0.0.1:3456/ \
  -H "Content-Type: application/json" \
  -d '{"model": "lite", "messages": [{"role": "user", "content": "你好"}]}'
