---
date: 2026-05-23T02:13:24+08:00
source: clipboard
chars: 860
---

litellm_settings:
  drop_params: true

model_list:
  - model_name: lite
    litellm_params:
      model: openai/lite
      api_base: https://spark-api-open.xf-yun.com/v1
      api_key: ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn
  - model_name: generalv3.5
    litellm_params:
      model: openai/generalv3.5
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
  supported_environments: ["openai", "anthropic"]
