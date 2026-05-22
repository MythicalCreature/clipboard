---
date: 2026-05-23T01:38:30+08:00
source: clipboard
chars: 234
---

cat > ~/.litellm/config.yaml << 'EOF'
model_list:
  - model_name: claude-opus-4-7
    litellm_params:
      model: spark-lite
      api_base: http://localhost:4000/v1
      api_key: sk-anything

litellm_settings:
  num_workers: 10
EOF
