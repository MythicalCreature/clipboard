---
date: 2026-05-24T00:41:55+08:00
source: clipboard
chars: 3165
---

cat > ~/clean-proxy/proxy.js << 'EOF'
const express = require('express');
const https = require('https');
const app = express();

app.use(express.json());

// 1. 模拟 Anthropic 的模型列表 API
app.get('/v1/models', (req, res) => {
    res.json({
        data: [
            {
                id: 'claude-3-haiku-20240307',
                object: 'model',
                created: 1711584000,
                owned_by: 'anthropic'
            }
        ]
    });
});

// 2. 模拟 Anthropic 的 Messages API（核心对话接口）
app.post('/v1/messages', async (req, res) => {
    try {
        // 清洗请求体，只保留最核心数据
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
                    
                    // 返回一个标准的 Anthropic 格式响应
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

// 3. 模拟其他可能被请求的路径，防止 404 错误中断 Claude Code 的验证流程
app.use((req, res) => {
    res.status(200).json({ status: 'ok' });
});

app.listen(3456, () => {
    console.log('✅ Anthropic全模拟代理已启动 → http://127.0.0.1:3456');
    console.log('📋 可用的模型: claude-3-haiku-20240307');
});
EOF

cd ~/clean-proxy && node proxy.js
