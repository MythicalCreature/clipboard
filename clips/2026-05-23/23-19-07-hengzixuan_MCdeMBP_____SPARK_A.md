---
date: 2026-05-23T23:19:07+08:00
source: clipboard
chars: 659
---

hengzixuan@MCdeMBP ~ % SPARK_API_KEY="ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn" litellm \
  --model openai/spark-lite \
  --api_base https://spark-api-open.xf-yun.com/v1 \
  --drop_params \
  --enforce_openai_response_format \
  --port 4000
23:18:57 - LiteLLM:WARNING: get_model_cost_map.py:271 - LiteLLM: Failed to fetch remote model cost map from https://raw.githubusercontent.com/BerriAI/litellm/main/model_prices_and_context_window.json: _ssl.c:1112: The handshake operation timed out. Falling back to local backup.
Usage: litellm [OPTIONS]
Try 'litellm --help' for help.

Error: No such option: --enforce_openai_response_format
zhengzixuan@MCdeMBP ~ % 

