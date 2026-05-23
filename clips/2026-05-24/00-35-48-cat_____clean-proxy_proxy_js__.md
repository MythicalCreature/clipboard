---
date: 2026-05-24T00:35:48+08:00
source: clipboard
chars: 2561
---

cat > ~/clean-proxy/proxy.js << 'EOF'
const express = require('express');
const https = require('https');
const app = express();

app.use(express.json());

// 模型列表
app.get('/v1/models', (req, res) => {
    res.json({
        object: 'list',
        data: [{ id: 'lite', object: 'model', created: 0, owned_by: 'spark' }]
    });
});

// 对话
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
                    // 使用最简洁、最接近 OpenAI 原始格式的响应
                    res.json({
                        id: sparkResponse.sid || 'chatcmpl-001',
                        object: 'chat.completion',
                        created: Math.floor(Date.now() / 1000),
                        model: 'lite',
                        choices: [{
                            index: 0,
                            message: {
                                role: 'assistant',
                                content: sparkResponse.choices[0].message.content
                            },
                            finish_reason: 'stop'
                        }],
                        usage: sparkResponse.usage || {}
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
    console.log('✅ 最终版代理已启动 → http://127.0.0.1:3456');
});
EOF

cd ~/clean-proxy && node proxy.js
