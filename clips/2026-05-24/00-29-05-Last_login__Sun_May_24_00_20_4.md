---
date: 2026-05-24T00:29:05+08:00
source: clipboard
chars: 455
---

Last login: Sun May 24 00:20:41 on ttys002
zhengzixuan@MCdeMBP ~ % curl -X POST http://127.0.0.1:3456/任意路径都可以 \
  -H "Content-Type: application/json" \
  -d '{
    "model": "lite",
    "messages": [{"role": "user", "content": "你好"}]
  }'
{"message":"Route POST:/%e4%bb%bb%e6%84%8f%e8%b7%af%e5%be%84%e9%83%bd%e5%8f%af%e4%bb%a5 not found","error":"Not Found","statusCode":404}%                       zhengzixuan@MCdeMBP ~ % 















