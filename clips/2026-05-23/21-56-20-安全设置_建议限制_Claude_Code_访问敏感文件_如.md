---
date: 2026-05-23T21:56:20+08:00
source: clipboard
chars: 190
---

安全设置：建议限制 Claude Code 访问敏感文件（如 .env），可在 settings.json 中配置 permissions。

json
"permissions": {
  "deny": ["Read(./.env)", "Read(./.env.*)"]
}
