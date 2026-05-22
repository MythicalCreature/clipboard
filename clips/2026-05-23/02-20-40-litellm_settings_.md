---
date: 2026-05-23T02:20:40+08:00
source: clipboard
chars: 677
---

litellm_settings:
  drop_params: true
  set_verbose: true

model_list:
  - model_name: lite
    litellm_params:
      model: openai/lite
      api_base: https://spark-api-open.xf-yun.com/v1
      api_key: ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn
  - model_name: claude-opus-4-7
    litellm_params:
      model: openai/lite
      api_base: https://spark-api-open.xf-yun.com/v1
      api_key: ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn
  - model_name: claude-sonnet-4-6
    litellm_params:
      model: openai/lite
      api_base: https://spark-api-open.xf-yun.com/v1
      api_key: ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn

router_settings:
  supported_environments: ["openai"]
