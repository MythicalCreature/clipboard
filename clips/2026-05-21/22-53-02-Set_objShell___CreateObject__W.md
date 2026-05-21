---
date: 2026-05-21T22:53:02+08:00
source: clipboard
chars: 155
---

Set objShell = CreateObject("Wscript.Shell")
objShell.Run "cmd /c python -m http.server 8000", 0
objShell.Run "http://localhost:8000/bbb.html"
WScript.Quit
