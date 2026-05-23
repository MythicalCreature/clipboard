---
date: 2026-05-24T00:44:40+08:00
source: clipboard
chars: 391
---

export ANTHROPIC_BASE_URL="http://127.0.0.1:3456"
export ANTHROPIC_AUTH_TOKEN="placeholder"
export ANTHROPIC_DEFAULT_SONNET_MODEL="lite"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="lite"
export ANTHROPIC_DEFAULT_OPUS_MODEL="lite"

# 创建一个假的 API 服务器，用管道处理请求
npx -y http-echo-server -p 3456 -c "cat | ~/spark-pipe.sh" &

sleep 2
claude --dangerously-skip-permissions
