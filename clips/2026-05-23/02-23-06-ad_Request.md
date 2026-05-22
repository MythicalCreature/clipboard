---
date: 2026-05-23T02:23:06+08:00
source: clipboard
chars: 1238
---

ad Request
INFO:     127.0.0.1:52030 - "HEAD / HTTP/1.1" 200 OK
02:22:59 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - 400: {'error': 'anthropic_messages: Invalid model name passed in model=claude-opus-4-7. Call `/v1/models` to view available models for your key.'}
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1052, in base_process_llm_request
    llm_call = await route_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/route_llm_request.py", line 563, in route_request
    raise ProxyModelNotFoundError(
litellm.proxy.route_llm_request.ProxyModelNotFoundError: 400: {'error': 'anthropic_messages: Invalid model name passed in model=claude-opus-4-7. Call `/v1/models` to view available models for your key.'}
INFO:     127.0.0.1:52041 - "POST /v1/messages?beta=true HTTP/1.1" 400 Bad Request

