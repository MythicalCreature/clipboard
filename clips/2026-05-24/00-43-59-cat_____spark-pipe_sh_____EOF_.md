---
date: 2026-05-24T00:43:59+08:00
source: clipboard
chars: 826
---

cat > ~/spark-pipe.sh << 'EOF'
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
