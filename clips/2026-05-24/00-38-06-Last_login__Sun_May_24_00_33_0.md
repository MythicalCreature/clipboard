---
date: 2026-05-24T00:38:06+08:00
source: clipboard
chars: 752
---

Last login: Sun May 24 00:33:09 on ttys000
zhengzixuan@MCdeMBP ~ % curl -v http://127.0.0.1:3456/v1/models
*   Trying 127.0.0.1:3456...
* Connected to 127.0.0.1 (127.0.0.1) port 3456
> GET /v1/models HTTP/1.1
> Host: 127.0.0.1:3456
> User-Agent: curl/8.6.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< X-Powered-By: Express
< Content-Type: application/json; charset=utf-8
< Content-Length: 107
< ETag: W/"6b-eSwZC9IETSE5ze9ouNwuvL2KHNU"
< Date: Sat, 23 May 2026 16:38:04 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
< 
* Connection #0 to host 127.0.0.1 left intact
{"object":"list","data":[{"id":"claude-3-haiku-20240307","object":"model","created":0,"owned_by":"spark"}]}%                                                    zhengzixuan@MCdeMBP ~ % 



