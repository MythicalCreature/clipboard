---
date: 2026-05-23T23:42:51+08:00
source: clipboard
chars: 2619
---

ase_client.py", line 1884, in post
    return await self.request(cast_to, opts, stream=stream, stream_cls=stream_cls)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_base_client.py", line 1669, in request
    raise self._make_status_error_from_response(err.response) from None
openai.BadRequestError: Error code: 400 - {'error': {'message': 'invalid data (sid: cha000ad455@dx19e5580b9939a4b812)', 'type': 'invalid_request_error', 'param': None, 'code': '10003'}}

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/main.py", line 622, in acompletion
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 1163, in async_streaming
    raise OpenAIError(
litellm.llms.openai.common_utils.OpenAIError: Error code: 400 - {'error': {'message': 'invalid data (sid: cha000ad455@dx19e5580b9939a4b812)', 'type': 'invalid_request_error', 'param': None, 'code': '10003'}}

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/proxy_server.py", line 7191, in chat_completion
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/main.py", line 641, in acompletion
    raise exception_type(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/exception_mapping_utils.py", line 2456, in exception_type
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/exception_mapping_utils.py", line 478, in exception_type
    raise BadRequestError(
litellm.exceptions.BadRequestError: litellm.BadRequestError: OpenAIException - invalid data (sid: cha000ad455@dx19e5580b9939a4b812)
INFO:     127.0.0.1:51232 - "POST /v1/chat/completions HTTP/1.1" 400 Bad Request

