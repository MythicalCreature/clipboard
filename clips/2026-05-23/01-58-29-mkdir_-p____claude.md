---
date: 2026-05-23T01:58:29+08:00
source: clipboard
chars: 184
---

mkdir -p ~/.claude

cat > ~/.claude/settings.json << 'EOF'
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://你的服务地址.com",
    "ANTHROPIC_API_KEY": "你的API密钥"
  }
}
EOF
