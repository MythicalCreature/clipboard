---
date: 2026-05-23T22:31:43+08:00
source: clipboard
chars: 1289
---

    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/responses_adapters/handler.py", line 146, in async_anthropic_messages_handler
    result = await litellm.aresponses(**responses_kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/responses/main.py", line 580, in aresponses
    raise litellm.exception_type(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/exception_mapping_utils.py", line 2456, in exception_type
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/exception_mapping_utils.py", line 552, in exception_type
    raise NotFoundError(
litellm.exceptions.NotFoundError: litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
INFO:     127.0.0.1:50159 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found


