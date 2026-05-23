---
date: 2026-05-24T01:06:10+08:00
source: clipboard
chars: 12483
---

Last login: Sun May 24 00:33:09 on ttys000
zhengzixuan@MCdeMBP ~ % curl -v http://127.0.0.1:3456/v1/models
*   Trying 127.0.0.1:3456...
* Connected to 127.0.0.1 (127.0.0.1) port 3456
> GET /v1/models HTTP/1.1
> Host: 127.0.0.1:3456
> User-Agent: curl/8.6.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< X-Powered-By: Express
< Content-Type: application/json; charset=utf-8
< Content-Length: 107
< ETag: W/"6b-eSwZC9IETSE5ze9ouNwuvL2KHNU"
< Date: Sat, 23 May 2026 16:38:04 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
< 
* Connection #0 to host 127.0.0.1 left intact
{"object":"list","data":[{"id":"claude-3-haiku-20240307","object":"model","created":0,"owned_by":"spark"}]}%                                                    zhengzixuan@MCdeMBP ~ % curl http://127.0.0.1:3456/v1/models
{"object":"list","data":[{"id":"claude-3-haiku-20240307","object":"model","created":1711584000,"owned_by":"anthropic"}]}%                                       zhengzixuan@MCdeMBP ~ % cat > ~/spark-pipe.sh << 'EOF'
#!/bin/bash
# 读取 Claude Code 发来的请求
read request
# 提取 messages 部分，只保留用户说的话
msg=$(echo "$request" | python3 -c "import sys,json; print(json.dumps({'model':'lite','messages':json.load(sys.stdin)['messages'],'stream':False}))")
# 发送清洗后的请求给讯飞，并把回复转换成 Claude Code 期望的格式
curl -s -X POST "https://spark-api-open.xf-yun.com/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn" \
  -d "$msg" | python3 -c "import sys,json; r=json.load(sys.stdin); print(json.dumps({'id':'msg_001','type':'message','role':'assistant','model':'lite','content':[{'type':'text','text':r['choices'][0]['message']['content']}],'stop_reason':'end_turn'}))"
EOF
zhengzixuan@MCdeMBP ~ % chmod +x ~/spark-pipe.sh
echo '{"messages":[{"role":"user","content":"你好"}]}' | ~/spark-pipe.sh
{"id": "msg_001", "type": "message", "role": "assistant", "model": "lite", "content": [{"type": "text", "text": "\u4f60\u597d\uff01\u6709\u4ec0\u4e48\u6211\u53ef\u4ee5\u5e2e\u52a9\u4f60\u7684\u5417\uff1f"}], "stop_reason": "end_turn"}
zhengzixuan@MCdeMBP ~ % export ANTHROPIC_BASE_URL="http://127.0.0.1:3456"
export ANTHROPIC_AUTH_TOKEN="placeholder"
export ANTHROPIC_DEFAULT_SONNET_MODEL="lite"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="lite"
export ANTHROPIC_DEFAULT_OPUS_MODEL="lite"

# 创建一个假的 API 服务器，用管道处理请求
npx -y http-echo-server -p 3456 -c "cat | ~/spark-pipe.sh" &

sleep 2
claude --dangerously-skip-permission
zsh: command not found: #
[1] 25930
[server] event: listening (port: NaN)
error: unknown option '--dangerously-skip-permission'
(Did you mean --dangerously-skip-permissions?)
zhengzixuan@MCdeMBP ~ % export ANTHROPIC_BASE_URL="http://127.0.0.1:3456"
export ANTHROPIC_AUTH_TOKEN="placeholder"
export ANTHROPIC_DEFAULT_SONNET_MODEL="lite"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="lite"
export ANTHROPIC_DEFAULT_OPUS_MODEL="lite"

# 创建一个假的 API 服务器，用管道处理请求
npx -y http-echo-server -p 3456 -c "cat | ~/spark-pipe.sh" &

sleep 2
claude --dangerously-skip-permission
zsh: command not found: #
[2] 25966
[server] event: error (msg: listen EADDRINUSE: address already in use -p)
[2]  + done       npx -y http-echo-server -p 3456 -c "cat | ~/spark-pipe.sh"
error: unknown option '--dangerously-skip-permission'
(Did you mean --dangerously-skip-permissions?)
zhengzixuan@MCdeMBP ~ % export ANTHROPIC_BASE_URL="http://127.0.0.1:3456"
export ANTHROPIC_AUTH_TOKEN="placeholder"
export ANTHROPIC_DEFAULT_SONNET_MODEL="lite"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="lite"
export ANTHROPIC_DEFAULT_OPUS_MODEL="lite"

# 创建一个假的 API 服务器，用管道处理请求
npx -y http-echo-server -p 3456 -c "cat | ~/spark-pipe.sh" &

sleep 2
claude --dangerously-skip-permissions
zsh: command not found: #
[2] 26010
[server] event: error (msg: listen EADDRINUSE: address already in use -p)
[2]  + done       npx -y http-echo-server -p 3456 -c "cat | ~/spark-pipe.sh"
╭─── Claude Code v2.1.150 ─────────────────────────────────────────────────────╮
│                                  │ Tips for getting started                  │
│           Welcome back!          │ Run /init to create a CLAUDE.md file wit… │
│                                  │ Note: You have launched claude in your h… │
│             ▗ ▗   ▖ ▖            │ ───────────────────────────────────────── │
│                                  │ What's new                                │
│               ▘▘ ▝▝              │ Internal infrastructure improvements (no… │
│                                  │ `/usage` now shows a per-category breakd… │
│   lite[1m] · API Usage Billing   │ `/diff` detail view can now be scrolled … │
│        /Users/zhengzixuan        │ /release-notes for more                   │
╰──────────────────────────────────────────────────────────────────────────────╯

❯ 你好                                                                          

⏺ There's an issue with the selected model (lite[1m]). It may not exist or you
  may not have access to it. Run /model to pick a different model.

✻ Baked for 0s

────────────────────────────────────────────────────────────────────────────────
❯  
────────────────────────────────────────────────────────────────────────────────
  Press Ctrl-C again to exit

Resume this session with:
claude --resume fb548215-05d5-4047-a898-1db733c4caa7
zhengzixuan@MCdeMBP ~ % export ANTHROPIC_BASE_URL="http://127.0.0.1:3456"
export ANTHROPIC_AUTH_TOKEN="placeholder"
export ANTHROPIC_DEFAULT_SONNET_MODEL="lite"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="lite"
export ANTHROPIC_DEFAULT_OPUS_MODEL="lite"

# 创建一个假的 API 服务器，用管道处理请求
npx -y http-echo-server -p 3456 -c "cat | ~/spark-pipe.sh" &

sleep 2
claude --dangerously-skip-permissions
zsh: command not found: #
[2] 26080
[server] event: error (msg: listen EADDRINUSE: address already in use -p)
[2]  + done       npx -y http-echo-server -p 3456 -c "cat | ~/spark-pipe.sh"
╭─── Claude Code v2.1.150 ─────────────────────────────────────────────────────╮
│                                  │ Tips for getting started                  │
│           Welcome back!          │ Run /init to create a CLAUDE.md file wit… │
│                                  │ Note: You have launched claude in your h… │
│             ▗ ▗   ▖ ▖            │ ───────────────────────────────────────── │
│                                  │ What's new                                │
│               ▘▘ ▝▝              │ Internal infrastructure improvements (no… │
│                                  │ `/usage` now shows a per-category breakd… │
│   lite[1m] · API Usage Billing   │ `/diff` detail view can now be scrolled … │
│        /Users/zhengzixuan        │ /release-notes for more                   │
╰──────────────────────────────────────────────────────────────────────────────╯

❯ 你好                                                                          

⏺ There's an issue with the selected model (lite[1m]). It may not exist or you
  may not have access to it. Run /model to pick a different model.

✻ Cooked for 0s

────────────────────────────────────────────────────────────────────────────────
❯  
────────────────────────────────────────────────────────────────────────────────
  Press Ctrl-C again to exit

Resume this session with:
claude --resume 36d49f2f-bc3d-4eb4-bcfa-9723f9896fd8
zhengzixuan@MCdeMBP ~ % cd ~/clean-proxy && node proxy.js
✅ Anthropic全模拟代理已启动 → http://127.0.0.1:3456
📋 可用的模型: claude-3-haiku-20240307
^C
zhengzixuan@MCdeMBP clean-proxy % 
zhengzixuan@MCdeMBP clean-proxy % mkdir -p ~/.continue && \
cat > ~/.continue/config.json << 'EOF'
{
  "models": [
    {
      "title": "Spark Lite",
      "provider": "openai",
      "model": "lite",
      "apiBase": "https://spark-api-open.xf-yun.com/v1",
      "apiKey": "ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn"
    }
  ]
}
EOF
zhengzixuan@MCdeMBP clean-proxy % npm install -g @skill-hub/cli

added 59 packages in 2s

35 packages are looking for funding
  run `npm fund` for details
zhengzixuan@MCdeMBP clean-proxy % skillhub

╭─────────────────────────────────╮
│   SkillHub CLI v0.1.0           │
│   Create & share AI agent skills │
╰─────────────────────────────────╯

Discover & Install:
  install    Install a skill to your agent (i, add)
  search     Search for skills (s, find)
  trending   Show trending skills (hot, popular)
  latest     Show recently added skills (new, recent)
  recommend  Get personalized recommendations (rec, suggest)
  top        Show all-time leaderboard (leaderboard, rank)

Create & Manage:
  login      Log in to SkillHub
  init       Initialize a new skill project
  push       Push local files to remote
  pull       Pull remote files to local
  status     Show local vs remote status
  publish    Publish skill to public directory
  list       List your skills (ls)
  whoami     Show current logged in user

Examples:
  $ skillhub install anthropics/skills/frontend-design
  $ skillhub search "react best practices"
  $ skillhub trending --limit 10

Run skillhub <command> --help for more info.

zhengzixuan@MCdeMBP clean-proxy % skillhub install summarize
✗ Skill not found: summarize
zhengzixuan@MCdeMBP clean-proxy % 
zhengzixuan@MCdeMBP clean-proxy % skillhub --version
0.1.0
zhengzixuan@MCdeMBP clean-proxy % skillhub search summarize

Found 10 skills:

#    Name       Category      Match  
─────────────────────────────────────
1.   summarize  development          
2.   summarize  development          
3.   summarize  development          
4.   summarize  productivity         
5.   summarize  development          
6.   summarize  development          
7.   summarize  development          
8.   summarize  development          
9.   summarize  development          
10.  summarize  development          

Full slugs for installation:
  1. moltbot-moltbot-summarize
  2. openclaw-openclaw-summarize
  3. molt-bot-clawdbot-summarize
  4. clawdbot-clawdbot-summarize
  5. hkuds-nanobot-summarize
  6. sipeed-picoclaw-summarize
  7. openclaw-skills-summary
  8. openclaw-skills-summarize-1-0-0
  9. letta-ai-lettabot-summarize
  10. gerstep-cybos-summarize

? Select a skill to install: › - Use arrow-keys. Return to submit.
❯   summarize [development]
    Summarize or extract text/transcripts from URLs, podcasts, …
    summarize [development]
    summarize [development]
    summarize [productivity]
    summarize [development]
    summarize [development]
    summarize [development]
    summarize [development]
    summarize [development]
  ↓ summarize [development]


