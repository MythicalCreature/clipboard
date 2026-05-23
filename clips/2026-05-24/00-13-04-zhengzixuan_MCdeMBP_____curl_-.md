---
date: 2026-05-24T00:13:04+08:00
source: clipboard
chars: 963
---

zhengzixuan@MCdeMBP ~ % curl -v -X POST http://127.0.0.1:3456/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "lite",
    "messages": [{"role": "user", "content": "你好"}]
  }'
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1:3456...
* Connected to 127.0.0.1 (127.0.0.1) port 3456
> POST /v1/chat/completions HTTP/1.1
> Host: 127.0.0.1:3456
> User-Agent: curl/8.6.0
> Accept: */*
> Content-Type: application/json
> Content-Length: 82
> 
< HTTP/1.1 404 Not Found
< access-control-allow-origin: *
< content-type: application/json; charset=utf-8
< content-length: 92
< Date: Sat, 23 May 2026 16:12:56 GMT
< Connection: keep-alive
< Keep-Alive: timeout=72
< 
* Connection #0 to host 127.0.0.1 left intact
{"message":"Route POST:/v1/chat/completions not found","error":"Not Found","statusCode":404}%                                                                   zhengzixuan@MCdeMBP ~ % 

