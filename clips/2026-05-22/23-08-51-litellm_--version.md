---
date: 2026-05-22T23:08:51+08:00
source: clipboard
chars: 4182
---

litellm --version
23:08:37 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
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
23:08:37 - LiteLLM Proxy:ERROR: guardrail_registry.py:185 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'
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
23:08:37 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.javelin: unsupported operand type(s) for |: '_TypedDictMeta' and '_TypedDictMeta'
23:08:37 - LiteLLM Proxy:ERROR: guardrail_registry.py:116 - Error processing litellm.proxy.guardrails.guardrail_hooks.aim: unsupported operand type(s) for |: 'type' and 'NoneType'

LiteLLM: Current Version = 1.83.9

zhengzixuan@MCdeMBP fenbi-helper-master % 

