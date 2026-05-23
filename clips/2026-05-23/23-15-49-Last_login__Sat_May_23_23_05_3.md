---
date: 2026-05-23T23:15:49+08:00
source: clipboard
chars: 1233
---

Last login: Sat May 23 23:05:33 on ttys001
ccr status%                                                                     zhengzixuan@MCdeMBP ~ % ccr status

📊 Claude Code Router Status
════════════════════════════════════════
✅ Status: Running
🆔 Process ID: 15212
🌐 Port: 3456
📡 API Endpoint: http://127.0.0.1:3456
📄 PID File: /Users/zhengzixuan/.claude-code-router/.claude-code-router.pid

🚀 Ready to use! Run the following commands:
   ccr code    # Start coding with Claude
   ccr stop   # Stop the service

zhengzixuan@MCdeMBP ~ % ccr config set spark-lite \
  --api-base "https://spark-api-open.xf-yun.com/v1" \
  --api-key "ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn" \
  --model "spark-lite" \
  --transformer "none"

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

zhengzixuan@MCdeMBP ~ % 

