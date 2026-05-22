---
date: 2026-05-23T01:26:16+08:00
source: clipboard
chars: 366
---

mkdir -p ~/.claude && cat > ~/.claude/settings.json << 'EOF'
{
  "env": {
    "ANTHROPIC_API_KEY": "ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn",
    "ANTHROPIC_BASE_URL": "http://localhost:4000/v1",
    "ANTHROPIC_MODEL": "spark-lite",
    "API_TIMEOUT_MS": "300000"
  },
  "primaryApiKey": "dummy",
  "permissions": {
    "defaultMode": "bypassPermissions"
  }
}
EOF
