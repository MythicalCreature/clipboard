---
date: 2026-05-23T22:01:41+08:00
source: clipboard
chars: 190
---

for f in ~/.zshrc ~/.zprofile ~/.zshenv ~/.zlogin ~/.zlogout ~/.bash_profile ~/.bashrc ~/.profile; do [ -f "$f" ] && grep -l "ANTHROPIC_API_KEY" "$f" 2>/dev/null && echo "Found in: $f"; done
