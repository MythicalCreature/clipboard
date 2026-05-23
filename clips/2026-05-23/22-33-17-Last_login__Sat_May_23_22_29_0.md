---
date: 2026-05-23T22:33:17+08:00
source: clipboard
chars: 29976
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

