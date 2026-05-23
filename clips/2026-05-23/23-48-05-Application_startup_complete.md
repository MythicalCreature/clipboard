---
date: 2026-05-23T23:48:05+08:00
source: clipboard
chars: 1380
---

  Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
23:47:31 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - 400: {'error': '/chat/completions: Invalid model name passed in model=lite. Call `/v1/models` to view available models for your key.'}
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/proxy_server.py", line 7191, in chat_completion
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1052, in base_process_llm_request
    llm_call = await route_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/route_llm_request.py", line 563, in route_request
    raise ProxyModelNotFoundError(
litellm.proxy.route_llm_request.ProxyModelNotFoundError: 400: {'error': '/chat/completions: Invalid model name passed in model=lite. Call `/v1/models` to view available models for your key.'}
INFO:     127.0.0.1:51271 - "POST /v1/chat/completions HTTP/1.1" 400 Bad Request
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     F
