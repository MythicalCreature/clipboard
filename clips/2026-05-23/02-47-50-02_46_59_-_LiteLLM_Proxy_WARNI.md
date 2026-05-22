---
date: 2026-05-23T02:47:50+08:00
source: clipboard
chars: 36709
---

02:46:59 - LiteLLM Proxy:WARNING: proxy_server.py:3669 - Key 'supported_environments' is not a valid argument for Router.__init__(). Ignoring this key.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
INFO:     ('127.0.0.1', 52376) - "WebSocket /v1/responses" 403
INFO:     connection rejected (403 Forbidden)
INFO:     connection closed
INFO:     ('127.0.0.1', 52377) - "WebSocket /v1/responses" 403
INFO:     connection rejected (403 Forbidden)
INFO:     connection closed
INFO:     ('127.0.0.1', 52379) - "WebSocket /v1/responses" 403
INFO:     connection rejected (403 Forbidden)
INFO:     connection closed
INFO:     ('127.0.0.1', 52380) - "WebSocket /v1/responses" 403
INFO:     connection rejected (403 Forbidden)
INFO:     connection closed
INFO:     ('127.0.0.1', 52381) - "WebSocket /v1/responses" 403
INFO:     connection rejected (403 Forbidden)
INFO:     connection closed
INFO:     ('127.0.0.1', 52383) - "WebSocket /v1/responses" 403
INFO:     connection rejected (403 Forbidden)
INFO:     connection closed
02:47:15 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 361, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_body, text=_body) from None
litellm.llms.custom_httpx.http_handler.MaskedHTTPStatusError: Client error '404 Not Found' for url 'https://spark-api-open.xf-yun.com/v1/responses'
For more information check: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/responses/main.py", line 558, in aresponses
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2421, in async_response_api_handler
    raise self._handle_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 4788, in _handle_error
    raise provider_config.get_error_class(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/base_llm/responses/transformation.py", line 214, in get_error_class
    raise BaseLLMException(
litellm.llms.base_llm.chat.transformation.BaseLLMException: 404 page not found

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/response_api_endpoints/endpoints.py", line 198, in responses_api
    response = await processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5144, in async_wrapper
    return await self._ageneric_api_call_with_fallbacks(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3800, in _ageneric_api_call_with_fallbacks
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3787, in _ageneric_api_call_with_fallbacks
    response = await self.async_function_with_fallbacks(**kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5613, in async_function_with_fallbacks
    return await self.async_function_with_fallbacks_common_utils(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5570, in async_function_with_fallbacks_common_utils
    raise original_exception
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5604, in async_function_with_fallbacks
    response = await self.async_function_with_retries(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5759, in async_function_with_retries
    self.should_retry_this_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5963, in should_retry_this_error
    raise error
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5710, in async_function_with_retries
    response = await self.make_call(original_function, *args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5878, in make_call
    response = await response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3927, in _ageneric_api_call_with_fallbacks_helper
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3913, in _ageneric_api_call_with_fallbacks_helper
    response = await response  # type: ignore
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
litellm.exceptions.NotFoundError: litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
INFO:     127.0.0.1:52384 - "POST /v1/responses HTTP/1.1" 404 Not Found
02:47:15 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 361, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_body, text=_body) from None
litellm.llms.custom_httpx.http_handler.MaskedHTTPStatusError: Client error '404 Not Found' for url 'https://spark-api-open.xf-yun.com/v1/responses'
For more information check: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/responses/main.py", line 558, in aresponses
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2421, in async_response_api_handler
    raise self._handle_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 4788, in _handle_error
    raise provider_config.get_error_class(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/base_llm/responses/transformation.py", line 214, in get_error_class
    raise BaseLLMException(
litellm.llms.base_llm.chat.transformation.BaseLLMException: 404 page not found

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/response_api_endpoints/endpoints.py", line 198, in responses_api
    response = await processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5144, in async_wrapper
    return await self._ageneric_api_call_with_fallbacks(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3800, in _ageneric_api_call_with_fallbacks
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3787, in _ageneric_api_call_with_fallbacks
    response = await self.async_function_with_fallbacks(**kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5613, in async_function_with_fallbacks
    return await self.async_function_with_fallbacks_common_utils(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5570, in async_function_with_fallbacks_common_utils
    raise original_exception
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5604, in async_function_with_fallbacks
    response = await self.async_function_with_retries(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5759, in async_function_with_retries
    self.should_retry_this_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5963, in should_retry_this_error
    raise error
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5710, in async_function_with_retries
    response = await self.make_call(original_function, *args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5878, in make_call
    response = await response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3927, in _ageneric_api_call_with_fallbacks_helper
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3913, in _ageneric_api_call_with_fallbacks_helper
    response = await response  # type: ignore
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
litellm.exceptions.NotFoundError: litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
INFO:     127.0.0.1:52386 - "POST /v1/responses HTTP/1.1" 404 Not Found
02:47:16 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 361, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_body, text=_body) from None
litellm.llms.custom_httpx.http_handler.MaskedHTTPStatusError: Client error '404 Not Found' for url 'https://spark-api-open.xf-yun.com/v1/responses'
For more information check: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/responses/main.py", line 558, in aresponses
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2421, in async_response_api_handler
    raise self._handle_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 4788, in _handle_error
    raise provider_config.get_error_class(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/base_llm/responses/transformation.py", line 214, in get_error_class
    raise BaseLLMException(
litellm.llms.base_llm.chat.transformation.BaseLLMException: 404 page not found

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/response_api_endpoints/endpoints.py", line 198, in responses_api
    response = await processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5144, in async_wrapper
    return await self._ageneric_api_call_with_fallbacks(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3800, in _ageneric_api_call_with_fallbacks
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3787, in _ageneric_api_call_with_fallbacks
    response = await self.async_function_with_fallbacks(**kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5613, in async_function_with_fallbacks
    return await self.async_function_with_fallbacks_common_utils(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5570, in async_function_with_fallbacks_common_utils
    raise original_exception
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5604, in async_function_with_fallbacks
    response = await self.async_function_with_retries(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5759, in async_function_with_retries
    self.should_retry_this_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5963, in should_retry_this_error
    raise error
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5710, in async_function_with_retries
    response = await self.make_call(original_function, *args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5878, in make_call
    response = await response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3927, in _ageneric_api_call_with_fallbacks_helper
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3913, in _ageneric_api_call_with_fallbacks_helper
    response = await response  # type: ignore
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
litellm.exceptions.NotFoundError: litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
INFO:     127.0.0.1:52387 - "POST /v1/responses HTTP/1.1" 404 Not Found
02:47:17 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 361, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_body, text=_body) from None
litellm.llms.custom_httpx.http_handler.MaskedHTTPStatusError: Client error '404 Not Found' for url 'https://spark-api-open.xf-yun.com/v1/responses'
For more information check: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/responses/main.py", line 558, in aresponses
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2421, in async_response_api_handler
    raise self._handle_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 4788, in _handle_error
    raise provider_config.get_error_class(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/base_llm/responses/transformation.py", line 214, in get_error_class
    raise BaseLLMException(
litellm.llms.base_llm.chat.transformation.BaseLLMException: 404 page not found

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/response_api_endpoints/endpoints.py", line 198, in responses_api
    response = await processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5144, in async_wrapper
    return await self._ageneric_api_call_with_fallbacks(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3800, in _ageneric_api_call_with_fallbacks
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3787, in _ageneric_api_call_with_fallbacks
    response = await self.async_function_with_fallbacks(**kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5613, in async_function_with_fallbacks
    return await self.async_function_with_fallbacks_common_utils(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5570, in async_function_with_fallbacks_common_utils
    raise original_exception
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5604, in async_function_with_fallbacks
    response = await self.async_function_with_retries(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5759, in async_function_with_retries
    self.should_retry_this_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5963, in should_retry_this_error
    raise error
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5710, in async_function_with_retries
    response = await self.make_call(original_function, *args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5878, in make_call
    response = await response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3927, in _ageneric_api_call_with_fallbacks_helper
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3913, in _ageneric_api_call_with_fallbacks_helper
    response = await response  # type: ignore
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
litellm.exceptions.NotFoundError: litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
INFO:     127.0.0.1:52388 - "POST /v1/responses HTTP/1.1" 404 Not Found
02:47:18 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 361, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_body, text=_body) from None
litellm.llms.custom_httpx.http_handler.MaskedHTTPStatusError: Client error '404 Not Found' for url 'https://spark-api-open.xf-yun.com/v1/responses'
For more information check: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/responses/main.py", line 558, in aresponses
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2421, in async_response_api_handler
    raise self._handle_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 4788, in _handle_error
    raise provider_config.get_error_class(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/base_llm/responses/transformation.py", line 214, in get_error_class
    raise BaseLLMException(
litellm.llms.base_llm.chat.transformation.BaseLLMException: 404 page not found

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/response_api_endpoints/endpoints.py", line 198, in responses_api
    response = await processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5144, in async_wrapper
    return await self._ageneric_api_call_with_fallbacks(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3800, in _ageneric_api_call_with_fallbacks
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3787, in _ageneric_api_call_with_fallbacks
    response = await self.async_function_with_fallbacks(**kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5613, in async_function_with_fallbacks
    return await self.async_function_with_fallbacks_common_utils(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5570, in async_function_with_fallbacks_common_utils
    raise original_exception
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5604, in async_function_with_fallbacks
    response = await self.async_function_with_retries(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5759, in async_function_with_retries
    self.should_retry_this_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5963, in should_retry_this_error
    raise error
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5710, in async_function_with_retries
    response = await self.make_call(original_function, *args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5878, in make_call
    response = await response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3927, in _ageneric_api_call_with_fallbacks_helper
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3913, in _ageneric_api_call_with_fallbacks_helper
    response = await response  # type: ignore
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
litellm.exceptions.NotFoundError: litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
INFO:     127.0.0.1:52389 - "POST /v1/responses HTTP/1.1" 404 Not Found
02:47:22 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 361, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_body, text=_body) from None
litellm.llms.custom_httpx.http_handler.MaskedHTTPStatusError: Client error '404 Not Found' for url 'https://spark-api-open.xf-yun.com/v1/responses'
For more information check: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/responses/main.py", line 558, in aresponses
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2421, in async_response_api_handler
    raise self._handle_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 4788, in _handle_error
    raise provider_config.get_error_class(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/base_llm/responses/transformation.py", line 214, in get_error_class
    raise BaseLLMException(
litellm.llms.base_llm.chat.transformation.BaseLLMException: 404 page not found

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/response_api_endpoints/endpoints.py", line 198, in responses_api
    response = await processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5144, in async_wrapper
    return await self._ageneric_api_call_with_fallbacks(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3800, in _ageneric_api_call_with_fallbacks
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3787, in _ageneric_api_call_with_fallbacks
    response = await self.async_function_with_fallbacks(**kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5613, in async_function_with_fallbacks
    return await self.async_function_with_fallbacks_common_utils(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5570, in async_function_with_fallbacks_common_utils
    raise original_exception
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5604, in async_function_with_fallbacks
    response = await self.async_function_with_retries(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5759, in async_function_with_retries
    self.should_retry_this_error(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5963, in should_retry_this_error
    raise error
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5710, in async_function_with_retries
    response = await self.make_call(original_function, *args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 5878, in make_call
    response = await response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3927, in _ageneric_api_call_with_fallbacks_helper
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/router.py", line 3913, in _ageneric_api_call_with_fallbacks_helper
    response = await response  # type: ignore
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
litellm.exceptions.NotFoundError: litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found. Received Model Group=lite
Available Model Group Fallbacks=None
INFO:     127.0.0.1:52390 - "POST /v1/responses HTTP/1.1" 404 Not Found


