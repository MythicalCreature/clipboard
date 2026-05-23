---
date: 2026-05-23T23:16:02+08:00
source: clipboard
chars: 348
---

curl -X POST "https://spark-api-open.xf-yun.com/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn" \
  -d '{
    "model": "spark-lite",
    "messages": [
      {
        "role": "user",
        "content": "你好，请用一句话介绍你自己"
      }
    ]
  }'
