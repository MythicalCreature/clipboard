---
date: 2026-05-23T22:38:52+08:00
source: clipboard
chars: 104432
---

Last login: Sat May 23 22:29:01 on ttys001
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm \
  --model openai/spark-lite \
  --api_base https://spark-api-open.xf-yun.com/v1 \
  --drop_params \
  --add_key \
  --port=4000
22:30:51 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/__init__.py", line 5, in <module>
    from .javelin import JavelinGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/javelin.py", line 16, in <module>
    from litellm.types.proxy.guardrails.guardrail_hooks.javelin import (
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 78, in <module>
    class JavelinGuardResponse(TypedDict):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 82, in JavelinGuardResponse
    JavelinPromptInjectionAssessment
TypeError: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:30:51 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/__init__.py", line 5, in <module>
    from .aim import AimGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 42, in <module>
    class AimGuardrail(CustomGuardrail):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 187, in AimGuardrail
    ) -> dict | None:
TypeError: unsupported operand type(s) for |: 'type' and 'NoneType'
22:30:51 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:30:51 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [11080]
INFO:     Waiting for application startup.

   ██╗     ██╗████████╗███████╗██╗     ██╗     ███╗   ███╗
   ██║     ██║╚══██╔══╝██╔════╝██║     ██║     ████╗ ████║
   ██║     ██║   ██║   █████╗  ██║     ██║     ██╔████╔██║
   ██║     ██║   ██║   ██╔══╝  ██║     ██║     ██║╚██╔╝██║
   ███████╗██║   ██║   ███████╗███████╗███████╗██║ ╚═╝ ██║
   ╚══════╝╚═╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝     ╚═╝


#------------------------------------------------------------#
#                                                            #
#           'It would help me if you could add...'            #
#        https://github.com/BerriAI/litellm/issues/new        #
#                                                            #
#------------------------------------------------------------#

 Thank you for using LiteLLM! - Krrish & Ishaan



Give Feedback / Get Help: https://github.com/BerriAI/litellm/issues/new


INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
INFO:     127.0.0.1:50155 - "HEAD / HTTP/1.1" 200 OK
22:31:36 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
22:31:36 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2412, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
^CINFO:     Application shutdown complete.
INFO:     Finished server process [11080]
^C
zhengzixuan@MCdeMBP ~ % 
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm \
  --model openai/spark-lite \
  --api_base https://spark-api-open.xf-yun.com/v1 \
  --drop_params \
  --add_key \
  --port=4000
22:32:54 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/__init__.py", line 5, in <module>
    from .javelin import JavelinGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/javelin.py", line 16, in <module>
    from litellm.types.proxy.guardrails.guardrail_hooks.javelin import (
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 78, in <module>
    class JavelinGuardResponse(TypedDict):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 82, in JavelinGuardResponse
    JavelinPromptInjectionAssessment
TypeError: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:32:54 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/__init__.py", line 5, in <module>
    from .aim import AimGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 42, in <module>
    class AimGuardrail(CustomGuardrail):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 187, in AimGuardrail
    ) -> dict | None:
TypeError: unsupported operand type(s) for |: 'type' and 'NoneType'
22:32:54 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:32:54 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [11541]
INFO:     Waiting for application startup.

   ██╗     ██╗████████╗███████╗██╗     ██╗     ███╗   ███╗
   ██║     ██║╚══██╔══╝██╔════╝██║     ██║     ████╗ ████║
   ██║     ██║   ██║   █████╗  ██║     ██║     ██╔████╔██║
   ██║     ██║   ██║   ██╔══╝  ██║     ██║     ██║╚██╔╝██║
   ███████╗██║   ██║   ███████╗███████╗███████╗██║ ╚═╝ ██║
   ╚══════╝╚═╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝     ╚═╝


#------------------------------------------------------------#
#                                                            #
#           'It would help me if you could add...'            #
#        https://github.com/BerriAI/litellm/issues/new        #
#                                                            #
#------------------------------------------------------------#

 Thank you for using LiteLLM! - Krrish & Ishaan



Give Feedback / Get Help: https://github.com/BerriAI/litellm/issues/new


INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
INFO:     127.0.0.1:50179 - "HEAD / HTTP/1.1" 200 OK
22:33:06 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50183 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
22:33:06 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2412, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50183 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [11541]
zhengzixuan@MCdeMBP ~ % 
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm \
  --model openai/spark-lite \
  --api_base https://spark-api-open.xf-yun.com/v1 \
  --drop_params \
  --add_key \
  --port=4000
22:34:19 - LiteLLM:WARNING: get_model_cost_map.py:271 - LiteLLM: Failed to fetch remote model cost map from https://raw.githubusercontent.com/BerriAI/litellm/main/model_prices_and_context_window.json: The read operation timed out. Falling back to local backup.
22:34:20 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/__init__.py", line 5, in <module>
    from .javelin import JavelinGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/javelin.py", line 16, in <module>
    from litellm.types.proxy.guardrails.guardrail_hooks.javelin import (
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 78, in <module>
    class JavelinGuardResponse(TypedDict):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 82, in JavelinGuardResponse
    JavelinPromptInjectionAssessment
TypeError: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:34:20 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/__init__.py", line 5, in <module>
    from .aim import AimGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 42, in <module>
    class AimGuardrail(CustomGuardrail):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 187, in AimGuardrail
    ) -> dict | None:
TypeError: unsupported operand type(s) for |: 'type' and 'NoneType'
22:34:20 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:34:20 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [11599]
INFO:     Waiting for application startup.

   ██╗     ██╗████████╗███████╗██╗     ██╗     ███╗   ███╗
   ██║     ██║╚══██╔══╝██╔════╝██║     ██║     ████╗ ████║
   ██║     ██║   ██║   █████╗  ██║     ██║     ██╔████╔██║
   ██║     ██║   ██║   ██╔══╝  ██║     ██║     ██║╚██╔╝██║
   ███████╗██║   ██║   ███████╗███████╗███████╗██║ ╚═╝ ██║
   ╚══════╝╚═╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝     ╚═╝


#------------------------------------------------------------#
#                                                            #
#            'This product would be better if...'             #
#        https://github.com/BerriAI/litellm/issues/new        #
#                                                            #
#------------------------------------------------------------#

 Thank you for using LiteLLM! - Krrish & Ishaan



Give Feedback / Get Help: https://github.com/BerriAI/litellm/issues/new


INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
INFO:     127.0.0.1:50201 - "HEAD / HTTP/1.1" 200 OK
22:34:31 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50209 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
22:34:32 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2412, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50209 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [11599]
^[[A%                                                                           zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm \
  --model openai/spark-lite \
  --api_base https://spark-api-open.xf-yun.com/v1 \
  --drop_params \
  --add_key \
  --port=4000
^CTraceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/bin/litellm", line 5, in <module>
    from litellm import run_server
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/__init__.py", line 1145, in <module>
    from .llms.anthropic.common_utils import AnthropicModelInfo
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/__init__.py", line 4, in <module>
    from .chat.transformation import AnthropicConfig
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/chat/__init__.py", line 1, in <module>
    from .handler import AnthropicChatCompletion, ModelResponseIterator
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/chat/handler.py", line 26, in <module>
    from litellm.anthropic_beta_headers_manager import (
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/anthropic_beta_headers_manager.py", line 32, in <module>
    from litellm.litellm_core_utils.litellm_logging import verbose_logger
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/litellm_logging.py", line 143, in <module>
    from ..integrations.gcs_bucket.gcs_bucket import GCSBucketLogger
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/integrations/gcs_bucket/gcs_bucket.py", line 15, in <module>
    from litellm.proxy._types import CommonProxyErrors
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/_types.py", line 2406, in <module>
    class LiteLLM_DeletedVerificationToken(LiteLLM_VerificationToken):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pydantic/_internal/_model_construction.py", line 255, in __new__
    complete_model_class(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pydantic/_internal/_model_construction.py", line 648, in complete_model_class
    schema = gen_schema.generate_schema(cls)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pydantic/_internal/_generate_schema.py", line 729, in generate_schema
    schema = self._generate_schema_inner(obj)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pydantic/_internal/_generate_schema.py", line 1023, in _generate_schema_inner
    return self._model_schema(obj)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pydantic/_internal/_generate_schema.py", line 764, in _model_schema
    if cls.__pydantic_fields_complete__ or cls is BaseModel_:
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pydantic/_internal/_model_construction.py", line 348, in __pydantic_fields_complete__
    return all(field_info._complete for field_info in field_infos.values())
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pydantic/_internal/_model_construction.py", line 348, in <genexpr>
    return all(field_info._complete for field_info in field_infos.values())
KeyboardInterrupt

zhengzixuan@MCdeMBP ~ % 
zhengzixuan@MCdeMBP ~ % 
zhengzixuan@MCdeMBP ~ % 
zhengzixuan@MCdeMBP ~ % 
zhengzixuan@MCdeMBP ~ % 
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm \
  --model openai/spark-lite \
  --api_base https://spark-api-open.xf-yun.com/v1 \
  --drop_params \
  --add_key \
  --port=4000
22:35:18 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/__init__.py", line 5, in <module>
    from .javelin import JavelinGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/javelin.py", line 16, in <module>
    from litellm.types.proxy.guardrails.guardrail_hooks.javelin import (
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 78, in <module>
    class JavelinGuardResponse(TypedDict):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 82, in JavelinGuardResponse
    JavelinPromptInjectionAssessment
TypeError: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:35:18 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/__init__.py", line 5, in <module>
    from .aim import AimGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 42, in <module>
    class AimGuardrail(CustomGuardrail):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 187, in AimGuardrail
    ) -> dict | None:
TypeError: unsupported operand type(s) for |: 'type' and 'NoneType'
22:35:18 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:35:18 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [11642]
INFO:     Waiting for application startup.

   ██╗     ██╗████████╗███████╗██╗     ██╗     ███╗   ███╗
   ██║     ██║╚══██╔══╝██╔════╝██║     ██║     ████╗ ████║
   ██║     ██║   ██║   █████╗  ██║     ██║     ██╔████╔██║
   ██║     ██║   ██║   ██╔══╝  ██║     ██║     ██║╚██╔╝██║
   ███████╗██║   ██║   ███████╗███████╗███████╗██║ ╚═╝ ██║
   ╚══════╝╚═╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝     ╚═╝


#------------------------------------------------------------#
#                                                            #
#               'A feature I really want is...'               #
#        https://github.com/BerriAI/litellm/issues/new        #
#                                                            #
#------------------------------------------------------------#

 Thank you for using LiteLLM! - Krrish & Ishaan



Give Feedback / Get Help: https://github.com/BerriAI/litellm/issues/new


INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
INFO:     127.0.0.1:50222 - "HEAD / HTTP/1.1" 200 OK
22:35:30 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50232 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
22:35:30 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2412, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50232 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [11642]
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm \
  --model openai/spark-lite \
  --api_base https://spark-api-open.xf-yun.com/v1 \
  --drop_params \
  --add_key \
  --port=4000
22:36:59 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/__init__.py", line 5, in <module>
    from .javelin import JavelinGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/javelin.py", line 16, in <module>
    from litellm.types.proxy.guardrails.guardrail_hooks.javelin import (
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 78, in <module>
    class JavelinGuardResponse(TypedDict):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 82, in JavelinGuardResponse
    JavelinPromptInjectionAssessment
TypeError: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:36:59 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/__init__.py", line 5, in <module>
    from .aim import AimGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 42, in <module>
    class AimGuardrail(CustomGuardrail):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 187, in AimGuardrail
    ) -> dict | None:
TypeError: unsupported operand type(s) for |: 'type' and 'NoneType'
22:36:59 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:36:59 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [11711]
INFO:     Waiting for application startup.

   ██╗     ██╗████████╗███████╗██╗     ██╗     ███╗   ███╗
   ██║     ██║╚══██╔══╝██╔════╝██║     ██║     ████╗ ████║
   ██║     ██║   ██║   █████╗  ██║     ██║     ██╔████╔██║
   ██║     ██║   ██║   ██╔══╝  ██║     ██║     ██║╚██╔╝██║
   ███████╗██║   ██║   ███████╗███████╗███████╗██║ ╚═╝ ██║
   ╚══════╝╚═╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝     ╚═╝


#------------------------------------------------------------#
#                                                            #
#         'The worst thing about this product is...'          #
#        https://github.com/BerriAI/litellm/issues/new        #
#                                                            #
#------------------------------------------------------------#

 Thank you for using LiteLLM! - Krrish & Ishaan



Give Feedback / Get Help: https://github.com/BerriAI/litellm/issues/new


INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
INFO:     127.0.0.1:50252 - "HEAD / HTTP/1.1" 200 OK
22:37:05 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50262 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
22:37:05 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2412, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50262 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
^CINFO:     Shutting down
^CINFO:     Finished server process [11711]
ERROR:    Traceback (most recent call last):
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/asyncio/runners.py", line 44, in run
    return loop.run_until_complete(main)
  File "uvloop/loop.pyx", line 1512, in uvloop.loop.Loop.run_until_complete
  File "uvloop/loop.pyx", line 1505, in uvloop.loop.Loop.run_until_complete
  File "uvloop/loop.pyx", line 1379, in uvloop.loop.Loop.run_forever
  File "uvloop/loop.pyx", line 557, in uvloop.loop.Loop._run
  File "uvloop/loop.pyx", line 476, in uvloop.loop.Loop._on_idle
  File "uvloop/cbhandles.pyx", line 83, in uvloop.loop.Handle._run
  File "uvloop/cbhandles.pyx", line 63, in uvloop.loop.Handle._run
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/uvicorn/server.py", line 69, in serve
    await self._serve(sockets)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/contextlib.py", line 124, in __exit__
    next(self.gen)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/uvicorn/server.py", line 332, in capture_signals
    signal.raise_signal(captured_signal)
KeyboardInterrupt

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/starlette/routing.py", line 701, in lifespan
    await receive()
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/uvicorn/lifespan/on.py", line 137, in receive
    return await self.receive_queue.get()
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/asyncio/queues.py", line 166, in get
    await getter
asyncio.exceptions.CancelledError

^C
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm \
  --model openai/spark-lite \
  --api_base https://spark-api-open.xf-yun.com/v1 \
  --drop_params \
  --add_key \
  --port=4000
22:37:42 - LiteLLM:WARNING: get_model_cost_map.py:271 - LiteLLM: Failed to fetch remote model cost map from https://raw.githubusercontent.com/BerriAI/litellm/main/model_prices_and_context_window.json: The read operation timed out. Falling back to local backup.
22:37:44 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/__init__.py", line 5, in <module>
    from .javelin import JavelinGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/javelin/javelin.py", line 16, in <module>
    from litellm.types.proxy.guardrails.guardrail_hooks.javelin import (
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 78, in <module>
    class JavelinGuardResponse(TypedDict):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/types/proxy/guardrails/guardrail_hooks/javelin.py", line 82, in JavelinGuardResponse
    JavelinPromptInjectionAssessment
TypeError: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:37:44 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_registry.py", line 173, in get_guardrail_class_from_hooks
    module = importlib.import_module(module_path)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/__init__.py", line 5, in <module>
    from .aim import AimGuardrail
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 42, in <module>
    class AimGuardrail(CustomGuardrail):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/guardrails/guardrail_hooks/aim/aim.py", line 187, in AimGuardrail
    ) -> dict | None:
TypeError: unsupported operand type(s) for |: 'type' and 'NoneType'
22:37:44 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
22:37:44 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [11743]
INFO:     Waiting for application startup.

   ██╗     ██╗████████╗███████╗██╗     ██╗     ███╗   ███╗
   ██║     ██║╚══██╔══╝██╔════╝██║     ██║     ████╗ ████║
   ██║     ██║   ██║   █████╗  ██║     ██║     ██╔████╔██║
   ██║     ██║   ██║   ██╔══╝  ██║     ██║     ██║╚██╔╝██║
   ███████╗██║   ██║   ███████╗███████╗███████╗██║ ╚═╝ ██║
   ╚══════╝╚═╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝     ╚═╝


#------------------------------------------------------------#
#                                                            #
#              'I don't like how this works...'               #
#        https://github.com/BerriAI/litellm/issues/new        #
#                                                            #
#------------------------------------------------------------#

 Thank you for using LiteLLM! - Krrish & Ishaan



Give Feedback / Get Help: https://github.com/BerriAI/litellm/issues/new


INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
INFO:     127.0.0.1:50269 - "HEAD / HTTP/1.1" 200 OK
22:37:52 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50273 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
22:37:52 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2412, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50273 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
22:38:15 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2378, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50281 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
22:38:15 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/llm_http_handler.py", line 2412, in async_response_api_handler
    response = await async_httpx_client.post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 574, in post
    await _raise_masked_async_error(e, stream)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/custom_httpx/http_handler.py", line 363, in _raise_masked_async_error
    raise MaskedHTTPStatusError(e, message=_text, text=_text) from None
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
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/anthropic_endpoints/endpoints.py", line 53, in anthropic_response
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1065, in base_process_llm_request
    responses = await llm_responses
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 2097, in wrapper_async
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/utils.py", line 1896, in wrapper_async
    result = await original_function(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/anthropic/experimental_pass_through/messages/handler.py", line 286, in anthropic_messages
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
INFO:     127.0.0.1:50281 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [11743]
zhengzixuan@MCdeMBP ~ % 

