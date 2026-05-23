---
date: 2026-05-24T00:11:14+08:00
source: clipboard
chars: 1241
---

cat > proxy.js << 'EOF'
const express = require('express');
const { createProxyMiddleware } = require('http-proxy-middleware');

const app = express();

// 关键：解析 JSON 请求体
app.use(express.json());

// 代理中间件
app.use('/', (req, res, next) => {
  // 构建干净的请求体
  const cleanBody = {
    model: 'lite',
    messages: req.body.messages || [],
    stream: false
  };
  
  // 将清洗后的 body 挂载回 req
  req.body = cleanBody;
  next();
});

app.use('/', createProxyMiddleware({
  target: 'https://spark-api-open.xf-yun.com',
  changeOrigin: true,
  on: {
    proxyReq: (proxyReq, req, res) => {
      // 重新计算并设置 Content-Length
      const bodyString = JSON.stringify(req.body);
      proxyReq.setHeader('Content-Length', Buffer.byteLength(bodyString));
      
      // 设置正确的认证头
      proxyReq.setHeader('Authorization', 'Bearer ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn');
      
      // 强制指向正确的API路径
      proxyReq.path = '/v1/chat/completions';
      
      // 写入清洗后的请求体
      proxyReq.write(bodyString);
    }
  }
}));

app.listen(3456, () => {
  console.log('✨ 强化版Spark代理已启动 → http://127.0.0.1:3456');
});
EOF
