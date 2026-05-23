---
date: 2026-05-24T00:38:24+08:00
source: clipboard
chars: 3018
---

cat > ~/clean-proxy/proxy.js << 'EOF'
const express = require('express');
const https = require('https');
const app = express();

app.use(express.json());

// 模拟 Anthropic API 的模型列表响应
app.get('/v1/models', (req, res) => {
    res.json({
        data: [
            {
                id: 'claude-3-haiku-20240307',
                object: 'model',
                created: 1711584000,
                owned_by: 'anthropic',
                capabilities: {
                    vision: false,
                    tool_use: false,
                    streaming: false
                }
            }
        ]
    });
});

// 模拟 Anthropic Messages API 端点
app.post('/v1/messages', async (req, res) => {
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
                    const realContent = sparkResponse.choices[0].message.content;
                    
                    // 完全模拟 Anthropic Messages API 的响应格式
                    res.json({
                        id: 'msg_' + Date.now(),
                        type: 'message',
                        role: 'assistant',
                        model: 'claude-3-haiku-20240307',
                        content: [{
                            type: 'text',
                            text: realContent
                        }],
                        stop_reason: 'end_turn',
                        stop_sequence: null,
                        usage: {
                            input_tokens: sparkResponse.usage?.prompt_tokens || 0,
                            output_tokens: sparkResponse.usage?.completion_tokens || 0
                        }
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
    console.log('✅ Anthropic模拟代理已启动 → http://127.0.0.1:3456');
});
EOF

cd ~/clean-proxy && node proxy.js
