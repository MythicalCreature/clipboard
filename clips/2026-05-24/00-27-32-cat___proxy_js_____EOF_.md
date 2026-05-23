---
date: 2026-05-24T00:27:32+08:00
source: clipboard
chars: 1209
---

cat > proxy.js << 'EOF'
const express = require('express');
const https = require('https');
const app = express();
app.use(express.json());

app.post('/*', async (req, res) => {
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
        res.status(500).send({ error: e.message });
    });
    
    proxyReq.write(postData);
    proxyReq.end();
});

app.listen(3456, () => {
    console.log('✨ 终极清洗代理已启动 → http://127.0.0.1:3456');
});
EOF
