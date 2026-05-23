---
date: 2026-05-24T00:14:00+08:00
source: clipboard
chars: 4178
---

Last login: Sun May 24 00:10:44 on ttys001
zhengzixuan@MCdeMBP ~ % claude
╭─── Claude Code v2.1.150 ─────────────────────────────────────────────────────╮
│                                               │ Tips for getting started     │
│                 Welcome back!                 │ Run /init to create a CLAUD… │
│                                               │ Note: You have launched cla… │
│                   ▗ ▗   ▖ ▖                   │ ──────────────────────────── │
│                                               │ What's new                   │
│                     ▘▘ ▝▝                     │ Internal infrastructure imp… │
│                                               │ `/usage` now shows a per-ca… │
│   Opus 4.7 (1M context) · API Usage Billing   │ `/diff` detail view can now… │
│              /Users/zhengzixuan               │ /release-notes for more      │
╰──────────────────────────────────────────────────────────────────────────────╯

❯ 你好                                                                          
  ⎿  API Error: 400 Client Error

✻ Worked for 0s                                              

────────────────────────────────────────────────────────────────────────────────
❯  
────────────────────────────────────────────────────────────────────────────────
  Press Ctrl-C again to exit                                 

Resume this session with:
claude --resume e59a6976-2dad-4e75-8e1a-dfaff88e3c1c
^C%                                                                             zhengzixuan@MCdeMBP ~ % curl -v -X POST http://127.0.0.1:3456/v1/chat/completions \
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
{"message":"Route POST:/v1/chat/completions not found","error":"Not Found","statusCode":404}%                                                                   zhengzixuan@MCdeMBP ~ % curl -v -X POST http://127.0.0.1:3456/v1/chat/completions \
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
< Date: Sat, 23 May 2026 16:13:55 GMT
< Connection: keep-alive
< Keep-Alive: timeout=72
< 
* Connection #0 to host 127.0.0.1 left intact
{"message":"Route POST:/v1/chat/completions not found","error":"Not Found","statusCode":404}%                                                                   zhengzixuan@MCdeMBP ~ % 

