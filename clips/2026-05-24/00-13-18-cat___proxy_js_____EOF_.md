---
date: 2026-05-24T00:13:18+08:00
source: clipboard
chars: 1431
---

cat > proxy.js << 'EOF'
const express = require('express');
const { createProxyMiddleware } = require('http-proxy-middleware');

const app = express();
app.use(express.json());

// 创建代理中间件
const apiProxy = createProxyMiddleware({
  target: 'https://spark-api-open.xf-yun.com',
  changeOrigin: true,
  pathRewrite: {
    '^/v1/chat/completions': '/v1/chat/completions',
  },
  on: {
    proxyReq: (proxyReq, req, res) => {
      // 构建干净的请求体
      const cleanBody = {
        model: 'lite',
        messages: req.body.messages || [],
        stream: false
      };
      
      const bodyString = JSON.stringify(cleanBody);
      proxyReq.setHeader('Content-Type', 'application/json');
      proxyReq.setHeader('Content-Length', Buffer.byteLength(bodyString));
      proxyReq.setHeader('Authorization', 'Bearer ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn');
      
      // 写入清洗后的请求体
      proxyReq.write(bodyString);
    },
    proxyRes: (proxyRes, req, res) => {
      // 确保响应是JSON格式
      if (!proxyRes.headers['content-type']) {
        proxyRes.headers['content-type'] = 'application/json';
      }
    }
  }
});

// 确保所有请求都经过代理
app.use('/*', apiProxy);

app.listen(3456, () => {
  console.log('✨ 修复版Spark代理已启动 → http://127.0.0.1:3456');
  console.log('📡 所有请求都将转发至讯飞Spark API');
});
EOF

node proxy.js
