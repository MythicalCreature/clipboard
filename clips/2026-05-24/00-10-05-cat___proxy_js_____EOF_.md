---
date: 2026-05-24T00:10:05+08:00
source: clipboard
chars: 1461
---

cat > proxy.js << 'EOF'
const express = require('express');
const { createProxyMiddleware } = require('http-proxy-middleware');

const app = express();

app.use('/', createProxyMiddleware({
  target: 'https://spark-api-open.xf-yun.com',
  changeOrigin: true,
  on: {
    proxyReq: (proxyReq, req, res) => {
      // 清除可能引起冲突的请求头
      proxyReq.removeHeader('x-api-key');
      proxyReq.removeHeader('x-stainless-lang');
      proxyReq.removeHeader('x-stainless-arch');
      
      // 设置正确的认证头
      proxyReq.setHeader('Authorization', 'Bearer ETqUhynPAOZpFxmMfBSt:xWWbCpmluONOgYpHwygn');
      
      // 修改请求路径，确保指向正确的API端点
      proxyReq.path = '/v1/chat/completions';
      
      // 如果请求体存在，清理不支持的参数
      if (req.body) {
        const cleanBody = {
          model: req.body.model || 'lite',
          messages: req.body.messages,
          stream: req.body.stream || false
        };
        
        // 只有非流式请求才需要重写body
        if (!cleanBody.stream) {
          const bodyString = JSON.stringify(cleanBody);
          proxyReq.setHeader('Content-Length', Buffer.byteLength(bodyString));
          proxyReq.write(bodyString);
        }
      }
    }
  }
}));

app.listen(3456, () => {
  console.log('✨ Spark 代理已启动 → http://127.0.0.1:3456');
  console.log('📡 正在将请求转发至讯飞 Spark API');
});
EOF
