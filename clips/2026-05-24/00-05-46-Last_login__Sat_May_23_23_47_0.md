---
date: 2026-05-24T00:05:46+08:00
source: clipboard
chars: 69544
---

Last login: Sat May 23 23:47:06 on ttys000
zhengzixuan@MCdeMBP ~ % litellm
23:47:26 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
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
23:47:26 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
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
23:47:26 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
23:47:26 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [18276]
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
INFO:     Finished server process [18276]
zhengzixuan@MCdeMBP ~ % litellm
23:49:24 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
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
23:49:24 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
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
23:49:24 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
23:49:24 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [18327]
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
23:49:32 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - 400: {'error': '/chat/completions: Invalid model name passed in model=spark-lite. Call `/v1/models` to view available models for your key.'}
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/proxy_server.py", line 7191, in chat_completion
    result = await base_llm_response_processor.base_process_llm_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/common_request_processing.py", line 1052, in base_process_llm_request
    llm_call = await route_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/route_llm_request.py", line 563, in route_request
    raise ProxyModelNotFoundError(
litellm.proxy.route_llm_request.ProxyModelNotFoundError: 400: {'error': '/chat/completions: Invalid model name passed in model=spark-lite. Call `/v1/models` to view available models for your key.'}
INFO:     127.0.0.1:51292 - "POST /v1/chat/completions HTTP/1.1" 400 Bad Request
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [18327]
^C
zhengzixuan@MCdeMBP ~ % 
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm --model openai/spark-lite --api_base https://spark-api-open.xf-yun.com/v1 --drop_params --alias spark-lite --port 4000
23:50:48 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
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
23:50:48 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
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
23:50:48 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
23:50:48 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [18440]
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

23:51:19 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - litellm.BadRequestError: OpenAIException - invalid data (sid: cha000bdf3a@dx19e5588ae00b894812)
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 1113, in async_streaming
    headers, response = await self.make_openai_chat_completion_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 461, in make_openai_chat_completion_request
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 438, in make_openai_chat_completion_request
    await openai_aclient.chat.completions.with_raw_response.create(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_legacy_response.py", line 384, in wrapped
    return cast(LegacyAPIResponse[R], await func(*args, **kwargs))
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/resources/chat/completions/completions.py", line 2700, in create
    return await self._post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_base_client.py", line 1884, in post
    return await self.request(cast_to, opts, stream=stream, stream_cls=stream_cls)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_base_client.py", line 1669, in request
    raise self._make_status_error_from_response(err.response) from None
openai.BadRequestError: Error code: 400 - {'error': {'message': 'invalid data (sid: cha000bdf3a@dx19e5588ae00b894812)', 'type': 'invalid_request_error', 'param': None, 'code': '10003'}}

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/main.py", line 622, in acompletion
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 1163, in async_streaming
    raise OpenAIError(
litellm.llms.openai.common_utils.OpenAIError: Error code: 400 - {'error': {'message': 'invalid data (sid: cha000bdf3a@dx19e5588ae00b894812)', 'type': 'invalid_request_error', 'param': None, 'code': '10003'}}

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
litellm.exceptions.BadRequestError: litellm.BadRequestError: OpenAIException - invalid data (sid: cha000bdf3a@dx19e5588ae00b894812)
INFO:     127.0.0.1:51333 - "POST /v1/chat/completions HTTP/1.1" 400 Bad Request
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [18440]
^C
zhengzixuan@MCdeMBP ~ % 
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm --model openai/spark-lite --api_base https://spark-api-open.xf-yun.com/v1 --drop_params --alias spark-lite --port 4000
23:55:59 - LiteLLM:WARNING: get_model_cost_map.py:271 - LiteLLM: Failed to fetch remote model cost map from https://raw.githubusercontent.com/BerriAI/litellm/main/model_prices_and_context_window.json: _ssl.c:1112: The handshake operation timed out. Falling back to local backup.
23:56:01 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
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
23:56:01 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
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
23:56:01 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
23:56:01 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [18560]
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
23:56:23 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
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
INFO:     127.0.0.1:51360 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
23:56:23 - LiteLLM Proxy:ERROR: endpoints.py:121 - litellm.proxy.proxy_server.anthropic_response(): Exception occured - litellm.NotFoundError: NotFoundError: OpenAIException - 404 page not found
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
INFO:     127.0.0.1:51362 - "POST /v1/messages?beta=true HTTP/1.1" 404 Not Found
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [18560]
^C
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm --model openai/spark-lite --api_base https://spark-api-open.xf-yun.com/v1 --drop_params --alias spark-lite --port 4000
23:57:03 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
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
23:57:03 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
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
23:57:03 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
23:57:03 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [18597]
INFO:     Waiting for application startup.

   ██╗     ██╗████████╗███████╗██╗     ██╗     ███╗   ███╗
   ██║     ██║╚══██╔══╝██╔════╝██║     ██║     ████╗ ████║
   ██║     ██║   ██║   █████╗  ██║     ██║     ██╔████╔██║
   ██║     ██║   ██║   ██╔══╝  ██║     ██║     ██║╚██╔╝██║
   ███████╗██║   ██║   ███████╗███████╗███████╗██║ ╚═╝ ██║
   ╚══════╝╚═╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝     ╚═╝


#------------------------------------------------------------#
#                                                            #
#           'I get frustrated when the product...'            #
#        https://github.com/BerriAI/litellm/issues/new        #
#                                                            #
#------------------------------------------------------------#

 Thank you for using LiteLLM! - Krrish & Ishaan



Give Feedback / Get Help: https://github.com/BerriAI/litellm/issues/new


INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
23:58:16 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - litellm.BadRequestError: OpenAIException - invalid data (sid: cha000bdd79@dx19e558f0b1db8f3812)
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 1113, in async_streaming
    headers, response = await self.make_openai_chat_completion_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 461, in make_openai_chat_completion_request
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 438, in make_openai_chat_completion_request
    await openai_aclient.chat.completions.with_raw_response.create(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_legacy_response.py", line 384, in wrapped
    return cast(LegacyAPIResponse[R], await func(*args, **kwargs))
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/resources/chat/completions/completions.py", line 2700, in create
    return await self._post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_base_client.py", line 1884, in post
    return await self.request(cast_to, opts, stream=stream, stream_cls=stream_cls)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_base_client.py", line 1669, in request
    raise self._make_status_error_from_response(err.response) from None
openai.BadRequestError: Error code: 400 - {'error': {'message': 'invalid data (sid: cha000bdd79@dx19e558f0b1db8f3812)', 'type': 'invalid_request_error', 'param': None, 'code': '10003'}}

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/main.py", line 622, in acompletion
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 1163, in async_streaming
    raise OpenAIError(
litellm.llms.openai.common_utils.OpenAIError: Error code: 400 - {'error': {'message': 'invalid data (sid: cha000bdd79@dx19e558f0b1db8f3812)', 'type': 'invalid_request_error', 'param': None, 'code': '10003'}}

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
litellm.exceptions.BadRequestError: litellm.BadRequestError: OpenAIException - invalid data (sid: cha000bdd79@dx19e558f0b1db8f3812)
INFO:     127.0.0.1:51378 - "POST /v1/chat/completions HTTP/1.1" 400 Bad Request
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [18597]
^C
zhengzixuan@MCdeMBP ~ % 
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm --model openai/spark-lite --api_base https://spark-api-open.xf-yun.com/v1 --drop_params --alias spark-lite --port 4000
00:04:57 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
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
00:04:57 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
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
00:04:57 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
00:04:57 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [18766]
INFO:     Waiting for application startup.

   ██╗     ██╗████████╗███████╗██╗     ██╗     ███╗   ███╗
   ██║     ██║╚══██╔══╝██╔════╝██║     ██║     ████╗ ████║
   ██║     ██║   ██║   █████╗  ██║     ██║     ██╔████╔██║
   ██║     ██║   ██║   ██╔══╝  ██║     ██║     ██║╚██╔╝██║
   ███████╗██║   ██║   ███████╗███████╗███████╗██║ ╚═╝ ██║
   ╚══════╝╚═╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝     ╚═╝


#------------------------------------------------------------#
#                                                            #
#       'This feature doesn't meet my needs because...'       #
#        https://github.com/BerriAI/litellm/issues/new        #
#                                                            #
#------------------------------------------------------------#

 Thank you for using LiteLLM! - Krrish & Ishaan



Give Feedback / Get Help: https://github.com/BerriAI/litellm/issues/new


INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
00:05:05 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - litellm.BadRequestError: OpenAIException - invalid data (sid: cha000ae96f@dx19e559548699a4b812)
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 1113, in async_streaming
    headers, response = await self.make_openai_chat_completion_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 461, in make_openai_chat_completion_request
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 438, in make_openai_chat_completion_request
    await openai_aclient.chat.completions.with_raw_response.create(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_legacy_response.py", line 384, in wrapped
    return cast(LegacyAPIResponse[R], await func(*args, **kwargs))
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/resources/chat/completions/completions.py", line 2700, in create
    return await self._post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_base_client.py", line 1884, in post
    return await self.request(cast_to, opts, stream=stream, stream_cls=stream_cls)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_base_client.py", line 1669, in request
    raise self._make_status_error_from_response(err.response) from None
openai.BadRequestError: Error code: 400 - {'error': {'message': 'invalid data (sid: cha000ae96f@dx19e559548699a4b812)', 'type': 'invalid_request_error', 'param': None, 'code': '10003'}}

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/main.py", line 622, in acompletion
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 1163, in async_streaming
    raise OpenAIError(
litellm.llms.openai.common_utils.OpenAIError: Error code: 400 - {'error': {'message': 'invalid data (sid: cha000ae96f@dx19e559548699a4b812)', 'type': 'invalid_request_error', 'param': None, 'code': '10003'}}

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
litellm.exceptions.BadRequestError: litellm.BadRequestError: OpenAIException - invalid data (sid: cha000ae96f@dx19e559548699a4b812)
INFO:     127.0.0.1:51398 - "POST /v1/chat/completions HTTP/1.1" 400 Bad Request
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [18766]
zhengzixuan@MCdeMBP ~ % export SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
litellm --model openai/spark-lite --api_base https://spark-api-open.xf-yun.com/v1 --drop_params --alias spark-lite --port 4000
00:05:34 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
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
00:05:34 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
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
00:05:34 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
00:05:34 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
INFO:     Started server process [18783]
INFO:     Waiting for application startup.

   ██╗     ██╗████████╗███████╗██╗     ██╗     ███╗   ███╗
   ██║     ██║╚══██╔══╝██╔════╝██║     ██║     ████╗ ████║
   ██║     ██║   ██║   █████╗  ██║     ██║     ██╔████╔██║
   ██║     ██║   ██║   ██╔══╝  ██║     ██║     ██║╚██╔╝██║
   ███████╗██║   ██║   ███████╗███████╗███████╗██║ ╚═╝ ██║
   ╚══════╝╚═╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝     ╚═╝


#------------------------------------------------------------#
#                                                            #
#            'The thing I wish you improved is...'            #
#        https://github.com/BerriAI/litellm/issues/new        #
#                                                            #
#------------------------------------------------------------#

 Thank you for using LiteLLM! - Krrish & Ishaan



Give Feedback / Get Help: https://github.com/BerriAI/litellm/issues/new


INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:4000 (Press CTRL+C to quit)
00:05:39 - LiteLLM Proxy:ERROR: common_request_processing.py:1570 - litellm.proxy.proxy_server._handle_llm_api_exception(): Exception occured - litellm.BadRequestError: OpenAIException - invalid data (sid: cha000be827@dx19e5595ce2bb8f3812)
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 1113, in async_streaming
    headers, response = await self.make_openai_chat_completion_request(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/litellm_core_utils/logging_utils.py", line 297, in async_wrapper
    result = await func(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 461, in make_openai_chat_completion_request
    raise e
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 438, in make_openai_chat_completion_request
    await openai_aclient.chat.completions.with_raw_response.create(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_legacy_response.py", line 384, in wrapped
    return cast(LegacyAPIResponse[R], await func(*args, **kwargs))
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/resources/chat/completions/completions.py", line 2700, in create
    return await self._post(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_base_client.py", line 1884, in post
    return await self.request(cast_to, opts, stream=stream, stream_cls=stream_cls)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/openai/_base_client.py", line 1669, in request
    raise self._make_status_error_from_response(err.response) from None
openai.BadRequestError: Error code: 400 - {'error': {'message': 'invalid data (sid: cha000be827@dx19e5595ce2bb8f3812)', 'type': 'invalid_request_error', 'param': None, 'code': '10003'}}

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/main.py", line 622, in acompletion
    response = await init_response
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/llms/openai/openai.py", line 1163, in async_streaming
    raise OpenAIError(
litellm.llms.openai.common_utils.OpenAIError: Error code: 400 - {'error': {'message': 'invalid data (sid: cha000be827@dx19e5595ce2bb8f3812)', 'type': 'invalid_request_error', 'param': None, 'code': '10003'}}

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
litellm.exceptions.BadRequestError: litellm.BadRequestError: OpenAIException - invalid data (sid: cha000be827@dx19e5595ce2bb8f3812)
INFO:     127.0.0.1:51408 - "POST /v1/chat/completions HTTP/1.1" 400 Bad Request
^CINFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [18783]
zhengzixuan@MCdeMBP ~ % 

