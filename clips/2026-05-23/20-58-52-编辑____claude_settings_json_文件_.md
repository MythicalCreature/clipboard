---
date: 2026-05-23T20:58:52+08:00
source: clipboard
chars: 556
---

编辑 ~/.claude/settings.json 文件，填入类似下面的内容（注意替换成你自己的API Key）：

json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "你自己的API_KEY",
    "ANTHROPIC_BASE_URL": "https://api.siliconflow.cn",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "deepseek-ai/DeepSeek-V3.2",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "deepseek-ai/DeepSeek-R1",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "deepseek-ai/DeepSeek-V2.5"
  }
}
2. 跳过首次验证
编辑 ~/.claude.json 文件，加入这行内容：

json
{
  "hasCompletedOnboarding": true
}

