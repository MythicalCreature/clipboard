---
date: 2026-05-23T22:01:48+08:00
source: clipboard
chars: 281
---

ANTHROPIC_API_KEY=你的官方API密钥
zhengzixuan@MCdeMBP ~ % for f in ~/.zshrc ~/.zprofile ~/.zshenv ~/.zlogin ~/.zlogout ~/.bash_profile ~/.bashrc ~/.profile; do [ -f "$f" ] && grep -l "ANTHROPIC_API_KEY" "$f" 2>/dev/null && echo "Found in: $f"; done
zhengzixuan@MCdeMBP ~ % 


