---
date: 2026-05-23T02:33:44+08:00
source: clipboard
chars: 299
---

cat > ~/.codex/config.toml << 'EOF'
# 直接填入讯飞的 OpenAI 兼容地址
openai_base_url = "https://spark-api-open.xf-yun.com/v1"
# 使用我们之前 curl 验证成功的模型名
model = "lite"
# 沙盒模式：允许修改当前项目目录下的文件
sandbox_mode = "workspace-write"
EOF
