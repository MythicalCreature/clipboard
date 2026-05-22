---
date: 2026-05-22T23:08:05+08:00
source: clipboard
chars: 1767
---

 litellm --version
23:07:58 - LiteLLM:WARNING: get_model_cost_map.py:271 - LiteLLM: Failed to fetch remote model cost map from https://raw.githubusercontent.com/BerriAI/litellm/main/model_prices_and_context_window.json: The read operation timed out. Falling back to local backup.
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/proxy_cli.py", line 638, in run_server
    from .proxy_server import (
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/proxy_server.py", line 36, in <module>
    import websockets
ModuleNotFoundError: No module named 'websockets'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/bin/litellm", line 8, in <module>
    sys.exit(run_server())
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/click/core.py", line 1161, in __call__
    return self.main(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/click/core.py", line 1082, in main
    rv = self.invoke(ctx)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/click/core.py", line 1443, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/click/core.py", line 788, in invoke
    return __callback(*args, **kwargs)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/litellm/proxy/proxy_cli.py", line 645, in run_server
    raise ModuleNotFoundError(
ModuleNotFoundError: Missing dependency No module named 'websockets'. Run `pip install 'litellm[proxy]'`
zhengzixuan@MCdeMBP fenbi-helper-master % 

