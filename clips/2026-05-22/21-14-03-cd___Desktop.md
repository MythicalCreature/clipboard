---
date: 2026-05-22T21:14:03+08:00
source: clipboard
chars: 212
---

cd ~/Desktop
mkdir -p mockplus_origin
i=1
while read url; do
  curl -H "Referer: https://app.mockplus.cn/" -H "User-Agent: Mozilla/5.0" "$url" -o mockplus_origin/$(printf "%03d" $i).png
  ((i++))
done < links.txt
