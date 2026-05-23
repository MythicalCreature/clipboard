---
date: 2026-05-23T23:05:12+08:00
source: clipboard
chars: 4362
---

Last login: Sat May 23 22:53:31 on ttys000
zhengzixuan@MCdeMBP ~ % brew install go
✔︎ JSON API cask.jws.json                             Downloaded   16.8MB/ 16.8MB
✔︎ JSON API formula.jws.json                          Downloaded   32.6MB/ 32.6MB
Inspect the formula dependency plan before installing with `brew install --ask`.
Enable ask mode by setting `HOMEBREW_ASK=1`.
Hide these hints with `HOMEBREW_NO_ENV_HINTS=1` (see `man brew`).
==> Fetching downloads for: go
Warning: Bottle missing, falling back to the default domain...
==> Downloading https://ghcr.io/v2/homebrew/core/go/manifests/1.26.3
######################################################################### 100.0%
^CBottle go (1.26.3)                                 Downloading 323.6KB/ 64.0M

zhengzixuan@MCdeMBP ~ % cd Documents 
zhengzixuan@MCdeMBP Documents % ls
ClaudeCode		IDEA			执法法条和笔记
zhengzixuan@MCdeMBP Documents % cd ClaudeCode 
zhengzixuan@MCdeMBP ClaudeCode % ls
fenbiPaperTool.js
zhengzixuan@MCdeMBP ClaudeCode % git clone https://github.com/ni00/spark-to-anthropic-adapter.git

正克隆到 'spark-to-anthropic-adapter'...
Username for 'https://github.com': MythicalCreature
Password for 'https://MythicalCreature@github.com': 
remote: Invalid username or token. Password authentication is not supported for Git operations.
致命错误：'https://github.com/ni00/spark-to-anthropic-adapter.git/' 鉴权失败
zhengzixuan@MCdeMBP ClaudeCode % git clone https://github.com/ni00/spark-to-anthropic-adapter.git

正克隆到 'spark-to-anthropic-adapter'...
Username for 'https://github.com': MythicalCreature
Password for 'https://MythicalCreature@github.com': 
remote: Invalid username or token. Password authentication is not supported for Git operations.
致命错误：'https://github.com/ni00/spark-to-anthropic-adapter.git/' 鉴权失败
zhengzixuan@MCdeMBP ClaudeCode % git clone https://github.com/ni00/spark-to-anthropic-adapter.git

正克隆到 'spark-to-anthropic-adapter'...
Username for 'https://github.com': MythicalCreature
Password for 'https://MythicalCreature@github.com': 
remote: Invalid username or token. Password authentication is not supported for Git operations.
致命错误：'https://github.com/ni00/spark-to-anthropic-adapter.git/' 鉴权失败
zhengzixuan@MCdeMBP ClaudeCode % npm install -g @datartech/claude-code-router
npm warn deprecated node-domexception@1.0.0: Use your platform's native DOMException instead

added 162 packages in 5s

37 packages are looking for funding
  run `npm fund` for details
zhengzixuan@MCdeMBP ClaudeCode % ccr provider add spark-lite https://spark-api-open.xf-yun.com/v1/chat/completions ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn lite

Usage: ccr [command]

Commands:
  start         Start server 
  stop          Stop server
  restart       Restart server
  status        Show server status
  code          Execute claude command
  ui            Open the web UI in browser
  -v, version   Show version information
  -h, help      Show help information

Example:
  ccr start
  ccr code "Write a Hello World"
  ccr ui

zhengzixuan@MCdeMBP ClaudeCode % ccr start
Enter Provider Name: spark-lite
Enter Provider API KEY: ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn
Enter Provider URL: https://spark-api-open.xf-yun.com/v1/chat/completions
Enter MODEL Name: lite
undefined
Loaded JSON config from: /Users/zhengzixuan/.claude-code-router/config.json
register transformer: Anthropic (endpoint: /v1/messages)
register transformer: gemini (endpoint: /v1beta/models/:modelAndAction)
register transformer: vertex-gemini (endpoint: /v1/projects/:projectId/locations/:location/publishers/google/models/:modelAndAction)
register transformer: vertex-claude (endpoint: /v1/projects/:projectId/locations/:location/publishers/anthropic/models/:modelAndAction)
register transformer: deepseek (no endpoint)
register transformer: tooluse (no endpoint)
register transformer: openrouter (no endpoint)
register transformer: maxtoken (no endpoint)
register transformer: groq (no endpoint)
register transformer: cleancache (no endpoint)
register transformer: enhancetool (no endpoint)
register transformer: reasoning (no endpoint)
register transformer: sampling (no endpoint)
register transformer: maxcompletiontokens (no endpoint)
spark-lite provider registered
🚀 LLMs API server listening on http://127.0.0.1:3456


