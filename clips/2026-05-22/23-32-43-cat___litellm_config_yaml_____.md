---
date: 2026-05-22T23:32:43+08:00
source: clipboard
chars: 268
---

cat > litellm_config.yaml << 'EOF'
model_list:
  - model_name: lite
    litellm_params:
      model: openai/lite
      api_base: https://spark-api-open.xf-yun.com/v1
      api_key: 你的真实API密钥
      provider: openai

litellm_settings:
  drop_params: true
EOF
