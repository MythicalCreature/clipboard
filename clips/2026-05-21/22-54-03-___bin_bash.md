---
date: 2026-05-21T22:54:03+08:00
source: clipboard
chars: 108
---

#!/bin/bash
cd "$(dirname "$0")"
python3 -m http.server 8000 &
sleep 1
open "http://localhost:8000/bbb.html"
