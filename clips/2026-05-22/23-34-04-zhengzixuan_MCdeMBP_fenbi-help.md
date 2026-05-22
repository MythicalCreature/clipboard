---
date: 2026-05-22T23:34:04+08:00
source: clipboard
chars: 746
---

zhengzixuan@MCdeMBP fenbi-helper-master % curl http://localhost:4000/v1/chat/completions \
-H "Content-Type: application/json" \
-d '{"model":"lite","messages":[{"role":"user","content":"在吗"}]}'
{"id":"chatcmpl-ddf83e14-af6d-4458-8d3b-fd7cec41d7ce","created":1779464040,"model":"lite","object":"chat.completion","choices":[{"finish_reason":"stop","index":0,"message":{"content":"我在这里，很高兴能和你交流。有什么可以帮到你的吗？","role":"assistant","provider_specific_fields":{"refusal":null}},"provider_specific_fields":{}}],"usage":{"completion_tokens":13,"prompt_tokens":2,"total_tokens":15},"code":0,"message":"Success","sid":"cha000b464b@dx19e50526e31b8f3812"}%        zhengzixuan@MCdeMBP fenbi-helper-master % 
