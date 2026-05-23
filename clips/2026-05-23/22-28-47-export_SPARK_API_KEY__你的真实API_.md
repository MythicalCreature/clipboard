---
date: 2026-05-23T22:28:47+08:00
source: clipboard
chars: 180
---

export SPARK_API_KEY="你的真实API_KEY"
litellm \
  --model openai/spark-lite \
  --api_base https://spark-api-open.xf-yun.com/v1 \
  --drop_params \
  --add_key \
  --port 4000
