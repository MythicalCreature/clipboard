---
date: 2026-05-22T23:09:14+08:00
source: clipboard
chars: 267
---

cat > litellm_config.yaml << 'EOF'
model_list:
  - model_name: spark-lite
    litellm_params:
      model: lite
      api_base: https://spark-api-open.xf-yun.com/v1
      api_key: 你的星火API密钥
      provider: openai

litellm_settings:
  drop_params: true
EOF
