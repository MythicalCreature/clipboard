---
date: 2026-05-22T20:12:30+08:00
source: clipboard
chars: 2666
---

(async function() {
  console.log('🚀 开始批量截图导出摹客设计稿...');
  const viewport = document.querySelector('.viewport, .canvas-container, [class*="canvas"]');
  if (!viewport) {
    alert('未找到画布容器，请尝试放大页面或刷新后再试');
    return;
  }

  // 配置参数
  const step = 800; // 每次滚动的步长（根据你的画布大小调整）
  const delay = 800; // 每次截图的等待时间
  let count = 0;

  // 自动遍历画布并截图
  const maxScroll = viewport.scrollHeight;
  for (let y = 0; y < maxScroll; y += step) {
    viewport.scrollTop = y;
    await new Promise(resolve => setTimeout(resolve, delay));

    // 用Chrome的内置截图API
    const filename = `mockplus_capture_${String(++count).padStart(3, '0')}.png`;
    console.log(`正在截图: ${filename}`);

    // 执行截图（需要浏览器开启实验性API）
    try {
      await new Promise((resolve, reject) => {
        chrome.debugger.attach({ tabId: chrome.devtools.target.selectedTabId }, '1.3', () => {
          chrome.debugger.sendCommand({ tabId: chrome.devtools.target.selectedTabId }, 'Page.captureScreenshot', {
            format: 'png',
            quality: 100,
            clip: {
              x: viewport.scrollLeft,
              y: viewport.scrollTop,
              width: viewport.clientWidth,
              height: viewport.clientHeight,
              scale: 1
            }
          }, (result) => {
            if (result.data) {
              const link = document.createElement('a');
              link.href = `data:image/png;base64,${result.data}`;
              link.download = filename;
              link.click();
              resolve();
            } else {
              reject(new Error('截图失败'));
            }
            chrome.debugger.detach({ tabId: chrome.devtools.target.selectedTabId });
          });
        });
      });
    } catch (e) {
      // 备用方案：用canvas截图（兼容所有浏览器）
      const canvas = document.createElement('canvas');
      const ctx = canvas.getContext('2d');
      const scale = window.devicePixelRatio;
      canvas.width = viewport.clientWidth * scale;
      canvas.height = viewport.clientHeight * scale;
      ctx.scale(scale, scale);
      ctx.drawImage(viewport, 0, 0, viewport.clientWidth, viewport.clientHeight);
      
      const link = document.createElement('a');
      link.href = canvas.toDataURL('image/png');
      link.download = filename;
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }
  }

  alert(`🎉 已完成 ${count} 张截图导出！`);
})();
