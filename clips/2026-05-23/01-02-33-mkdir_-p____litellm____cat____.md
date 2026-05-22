---
date: 2026-05-23T01:02:33+08:00
source: clipboard
chars: 259
---

mkdir -p ~/.litellm && cat > ~/.litellm/config.yaml << 'EOF'
model_list:
  - model_name: claude-3-5-sonnet
    litellm_params:
      model: spark-lite
      api_base: http://localhost:4000/v1
      api_key: sk-anything

litellm_settings:
  num_workers: 10
EOF
