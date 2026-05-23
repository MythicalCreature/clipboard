---
date: 2026-05-23T22:21:25+08:00
source: clipboard
chars: 541
---

model_list:
  - model_name: spark-lite-proxy   # 改个内部唯一的名字，避免冲突
    litellm_params:
      model: openai/spark-lite    # 正确的讯飞官方模型名
      api_base: https://spark-api-open.xf-yun.com/v1
      api_key: os.environ/SPARK_API_KEY
    model_info:
      mode: chat                   # 明确告诉 LiteLLM 这是聊天模型
      supported_environments: ["openai"] # 只需要 openai 环境

router_settings:
  supported_environments: ["openai", "anthropic"] # 让 LiteLLM 能同时处理两种格式
