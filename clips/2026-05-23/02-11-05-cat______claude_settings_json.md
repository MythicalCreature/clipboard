---
date: 2026-05-23T02:11:05+08:00
source: clipboard
chars: 282
---

cat > ~/.claude/settings.json << 'EOF'
{
  "env": {
    "ANTHROPIC_BASE_URL": "http://localhost:4000",
    "ANTHROPIC_API_KEY": "sk-1234",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "lite",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "lite",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "lite"
  }
}
EOF
