---
date: 2026-05-24T00:35:13+08:00
source: clipboard
chars: 2403
---

cat > ~/clean-proxy/proxy.js << 'EOF'
const express = require('express');
const https = require('https');
const app = express();

app.use(express.json());

// 处理模型列表请求（Claude Code 启动时会验证这个）
app.get('/v1/models', (req, res) => {
    res.json({
        data: [
            { id: 'lite', object: 'model', owned_by: 'spark' }
        ]
    });
});

// 处理对话请求
app.post('/v1/chat/completions', async (req, res) => {
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
                    res.json({
                        id: sparkResponse.sid || 'msg_001',
                        object: 'chat.completion',
                        model: 'lite',
                        choices: [{
                            index: 0,
                            message: {
                                role: 'assistant',
                                content: sparkResponse.choices[0].message.content
                            },
                            finish_reason: 'stop'
                        }]
                    });
                } catch (e) {
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
    console.log('✅ 完美代理已启动 → http://127.0.0.1:3456');
});
EOF

cd ~/clean-proxy && node proxy.js
