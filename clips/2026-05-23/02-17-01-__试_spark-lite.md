---
date: 2026-05-23T02:17:01+08:00
source: clipboard
chars: 791
---

# 试 spark-lite
curl -s https://spark-api-open.xf-yun.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn" \
  -d '{"model":"spark-lite","messages":[{"role":"user","content":"hi"}]}'

# 试 generalv3
curl -s https://spark-api-open.xf-yun.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn" \
  -d '{"model":"generalv3","messages":[{"role":"user","content":"hi"}]}'

# 试 lite
curl -s https://spark-api-open.xf-yun.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn" \
  -d '{"model":"lite","messages":[{"role":"user","content":"hi"}]}'
