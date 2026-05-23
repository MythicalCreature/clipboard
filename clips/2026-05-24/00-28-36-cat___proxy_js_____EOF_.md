---
date: 2026-05-24T00:28:36+08:00
source: clipboard
chars: 2113
---

cat > proxy.js << 'EOF'
const http = require('http');
const https = require('https');

const server = http.createServer((req, res) => {
    // 只处理POST请求，忽略所有路径
    if (req.method !== 'POST') {
        res.writeHead(405, { 'Content-Type': 'application/json' });
        return res.end(JSON.stringify({ error: 'Method Not Allowed' }));
    }

    let body = '';
    req.on('data', chunk => { body += chunk; });
    req.on('end', () => {
        try {
            const original = JSON.parse(body);
            // 构建只含model和messages的纯净请求体
            const cleanBody = JSON.stringify({
                model: 'lite',
                messages: original.messages || []
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
                proxyRes.on('data', chunk => { data += chunk; });
                proxyRes.on('end', () => {
                    res.writeHead(proxyRes.statusCode, { 'Content-Type': 'application/json' });
                    res.end(data);
                });
            });

            proxyReq.on('error', (e) => {
                res.writeHead(500, { 'Content-Type': 'application/json' });
                res.end(JSON.stringify({ error: e.message }));
            });

            proxyReq.write(cleanBody);
            proxyReq.end();
        } catch (e) {
            res.writeHead(400, { 'Content-Type': 'application/json' });
            res.end(JSON.stringify({ error: 'Invalid JSON' }));
        }
    });
});

server.listen(3456, () => {
    console.log('✨ 终极纯净代理已启动 → http://127.0.0.1:3456');
});
EOF

node proxy.js
