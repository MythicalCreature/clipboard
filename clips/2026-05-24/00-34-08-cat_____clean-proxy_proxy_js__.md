---
date: 2026-05-24T00:34:08+08:00
source: clipboard
chars: 2282
---

cat > ~/clean-proxy/proxy.js << 'EOF'
const express = require('express');
const https = require('https');
const app = express();

app.use(express.json());

app.post('/', async (req, res) => {
    try {
        const cleanBody = JSON.stringify({
            model: 'lite',
            messages: req.body.messages || [],
            stream: false
        });
        
        const options = {
            hostname: 'spark-api-open.xf-yun.com',
            path: '/v1/chat/completions',
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Content-Length': Buffer.byteLength(cleanBody),
                'Authorization': 'Bearer ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn'
            }
        };
        
        const proxyReq = https.request(options, (proxyRes) => {
            let data = '';
            proxyRes.on('data', (chunk) => { data += chunk; });
            proxyRes.on('end', () => {
                try {
                    const sparkResponse = JSON.parse(data);
                    // 转换为类Anthropic格式，同时保留原始内容
                    const anthropicStyleResponse = {
                        id: sparkResponse.sid || 'msg_001',
                        type: 'message',
                        role: 'assistant',
                        content: [{
                            type: 'text',
                            text: sparkResponse.choices[0].message.content
                        }],
                        model: 'lite',
                        stop_reason: 'end_turn'
                    };
                    res.status(200).json(anthropicStyleResponse);
                } catch (e) {
                    // 如果转换失败，直接返回原始内容
                    res.status(200).send(data);
                }
            });
        });
        
        proxyReq.on('error', (e) => {
            res.status(500).send({ error: e.message });
        });
        
        proxyReq.write(cleanBody);
        proxyReq.end();
    } catch (e) {
        res.status(400).send({ error: 'Invalid JSON' });
    }
});

app.listen(3456, () => {
    console.log('✅ 转换版代理已启动 → http://127.0.0.1:3456');
});
EOF

cd ~/clean-proxy && node proxy.js
