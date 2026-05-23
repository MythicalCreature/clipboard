---
date: 2026-05-24T00:33:17+08:00
source: clipboard
chars: 1159
---

Last login: Sun May 24 00:29:42 on ttys001
zhengzixuan@MCdeMBP ~ % curl -v -X POST http://127.0.0.1:3456/ \
  -H "Content-Type: application/json" \
  -d '{"model": "lite", "messages": [{"role": "user", "content": "你好"}]}'
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1:3456...
* Connected to 127.0.0.1 (127.0.0.1) port 3456
> POST / HTTP/1.1
> Host: 127.0.0.1:3456
> User-Agent: curl/8.6.0
> Accept: */*
> Content-Type: application/json
> Content-Length: 70
> 
< HTTP/1.1 200 OK
< X-Powered-By: Express
< Content-Type: text/html; charset=utf-8
< Content-Length: 274
< ETag: W/"112-/0M/1O/g9B0IrR/PgatiwLA13Cw"
< Date: Sat, 23 May 2026 16:33:13 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
< 
* Connection #0 to host 127.0.0.1 left intact
{"code":0,"message":"Success","sid":"cha000b131f@dx19e55af0a4db894812","choices":[{"message":{"role":"assistant","content":"你好！很高兴见到你。有什么我可以帮助你的吗？"},"index":0}],"usage":{"prompt_tokens":1,"completion_tokens":12,"total_tokens":13}}%                                                                   zhengzixuan@MCdeMBP ~ % 

