---
date: 2026-05-24T00:13:29+08:00
source: clipboard
chars: 6703
---

Last login: Sat May 23 23:47:19 on ttys001
zhengzixuan@MCdeMBP ~ % claude
╭─── Claude Code v2.1.150 ─────────────────────────────────────────────────────╮
│                                               │ Tips for getting started     │
│                 Welcome back!                 │ Run /init to create a CLAUD… │
│                                               │ Note: You have launched cla… │
│                   ▗ ▗   ▖ ▖                   │ ──────────────────────────── │
│                                               │ What's new                   │
│                     ▘▘ ▝▝                     │ Internal infrastructure imp… │
│                                               │ `/usage` now shows a per-ca… │
│   Opus 4.7 (1M context) · API Usage Billing   │ `/diff` detail view can now… │
│              /Users/zhengzixuan               │ /release-notes for more      │
╰──────────────────────────────────────────────────────────────────────────────╯

❯ 你好                                                                          
  ⎿  API Error: 400 invalid data (sid: cha000bf2a4@dx19e559878b0b894812)

✻ Brewed for 0s                                              

────────────────────────────────────────────────────────────────────────────────
❯  
────────────────────────────────────────────────────────────────────────────────
  Press Ctrl-C again to exit                                 

Resume this session with:
claude --resume fe9e8c1b-f5ad-4826-9737-f75b97fc09fb
^C%                                                                             zhengzixuan@MCdeMBP ~ % mkdir ~/spark-proxy && cd ~/spark-proxy
zhengzixuan@MCdeMBP spark-proxy % npm init -y && npm install express http-proxy-middleware
Wrote to /Users/zhengzixuan/spark-proxy/package.json:

{
  "name": "spark-proxy",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}




added 77 packages in 1s

26 packages are looking for funding
  run `npm fund` for details
zhengzixuan@MCdeMBP spark-proxy % >....                                         
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
zhengzixuan@MCdeMBP spark-proxy % npm install express

up to date in 247ms

26 packages are looking for funding
  run `npm fund` for details
zhengzixuan@MCdeMBP spark-proxy % node proxy.js
✨ Spark 代理已启动 → http://127.0.0.1:3456
📡 正在将请求转发至讯飞 Spark API
^C
zhengzixuan@MCdeMBP spark-proxy % 
zhengzixuan@MCdeMBP spark-proxy % >....                                         
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
zhengzixuan@MCdeMBP spark-proxy % node proxy.js
✨ 强化版Spark代理已启动 → http://127.0.0.1:3456
^C
zhengzixuan@MCdeMBP spark-proxy % 
zhengzixuan@MCdeMBP spark-proxy % 
zhengzixuan@MCdeMBP spark-proxy % >....                                         

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
/Users/zhengzixuan/spark-proxy/node_modules/path-to-regexp/dist/index.js:108
                    throw new PathError(`Missing parameter name at index ${index}`, str);
                    ^

PathError [TypeError]: Missing parameter name at index 2: /*; visit https://git.new/pathToRegexpError for info
    at consumeUntil (/Users/zhengzixuan/spark-proxy/node_modules/path-to-regexp/dist/index.js:108:27)
    at parse (/Users/zhengzixuan/spark-proxy/node_modules/path-to-regexp/dist/index.js:140:26)
    at process (/Users/zhengzixuan/spark-proxy/node_modules/path-to-regexp/dist/index.js:263:56)
    at pathToRegexp (/Users/zhengzixuan/spark-proxy/node_modules/path-to-regexp/dist/index.js:274:5)
    at Object.match (/Users/zhengzixuan/spark-proxy/node_modules/path-to-regexp/dist/index.js:225:30)
    at matcher (/Users/zhengzixuan/spark-proxy/node_modules/router/lib/layer.js:86:23)
    at new Layer (/Users/zhengzixuan/spark-proxy/node_modules/router/lib/layer.js:93:62)
    at Function.use (/Users/zhengzixuan/spark-proxy/node_modules/router/index.js:398:19)
    at Function.<anonymous> (/Users/zhengzixuan/spark-proxy/node_modules/express/lib/application.js:222:21)
    at Array.forEach (<anonymous>) {
  originalPath: '/*'
}

Node.js v22.22.3
zhengzixuan@MCdeMBP spark-proxy % 

