---
date: 2026-05-22T23:29:03+08:00
source: clipboard
chars: 264
---

cat > litellm_config.yaml << 'EOF'
model_list:
  - model_name: lite
    litellm_params:
      model: lite
      api_base: https://spark-api-open.xf-yun.com/v1
      api_key: 你粘贴你的真实KEY
      provider: openai

litellm_settings:
  drop_params: true
EOF
