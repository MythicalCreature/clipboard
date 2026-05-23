---
date: 2026-05-24T00:28:05+08:00
source: clipboard
chars: 1558
---

cat > proxy.js << 'EOF'
const express = require('express');
const https = require('https');
const app = express();
app.use(express.json());

// 使用 app.all 和 '*' 来匹配所有请求，避免复杂的路由解析
app.all('*', async (req, res) => {
    // 只处理 POST 请求
    if (req.method !== 'POST') {
        return res.status(405).send({ error: 'Method Not Allowed' });
    }
    
    const cleanBody = {
        model: 'lite',
        messages: req.body.messages || []
    };
    const postData = JSON.stringify(cleanBody);
    
    const options = {
        hostname: 'spark-api-open.xf-yun.com',
        path: '/v1/chat/completions',
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'Content-Length': Buffer.byteLength(postData),
            'Authorization': 'Bearer ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn'
        }
    };
    
    const proxyReq = https.request(options, (proxyRes) => {
        let data = '';
        proxyRes.on('data', (chunk) => { data += chunk; });
        proxyRes.on('end', () => {
            res.status(proxyRes.statusCode).send(data);
        });
    });
    
    proxyReq.on('error', (e) => {
        console.error('代理请求失败:', e.message);
        res.status(500).send({ error: e.message });
    });
    
    proxyReq.write(postData);
    proxyReq.end();
});

app.listen(3456, () => {
    console.log('✨ 终极清洗代理已启动 → http://127.0.0.1:3456');
    console.log('📡 只接受POST请求，转发给讯飞Spark Lite');
});
EOF
