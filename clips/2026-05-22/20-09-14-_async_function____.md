---
date: 2026-05-22T20:09:14+08:00
source: clipboard
chars: 3279
---

(async function() {
  console.log('🚀 开始批量导出摹客设计稿为PNG...');

  // 1. 自动滚动页面，触发所有懒加载图片
  const scrollToBottom = () => new Promise(resolve => {
    let scrollHeight = document.body.scrollHeight;
    let scrollTop = 0;
    const step = 500;
    const interval = setInterval(() => {
      scrollTop += step;
      window.scrollTo(0, scrollTop);
      if (scrollTop >= scrollHeight) {
        clearInterval(interval);
        setTimeout(resolve, 1000); // 等待图片加载
      }
    }, 100);
  });
  await scrollToBottom();
  console.log('✅ 页面滚动完成，图片已全部加载');

  // 2. 抓取摹客所有画板元素（适配Mockplus的结构）
  // 适配摹客的画板容器，可根据实际情况调整选择器
  const artboards = Array.from(document.querySelectorAll('[data-artboard-id], .artboard, canvas[class*="artboard"]'));
  console.log(`📋 找到 ${artboards.length} 个画板`);

  if (artboards.length === 0) {
    alert('未找到画板元素，请尝试放大页面或手动滚动到所有设计稿可见区域后再试');
    return;
  }

  // 3. 逐个转换为PNG并下载
  for (let i = 0; i < artboards.length; i++) {
    const board = artboards[i];
    const filename = `mockplus_artboard_${String(i+1).padStart(3, '0')}.png`;

    try {
      // 方法A：如果是canvas元素，直接导出
      if (board.tagName === 'CANVAS') {
        const link = document.createElement('a');
        link.download = filename;
        link.href = board.toDataURL('image/png');
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        console.log(`✅ 已下载(canvas): ${filename}`);
      } 
      // 方法B：如果是div容器，先转成canvas再导出
      else {
        // 使用html2canvas逻辑简化版，这里用dom-to-image的思路
        // 先获取元素的背景图或内部img
        const img = board.querySelector('img');
        if (img && img.src) {
          const canvas = document.createElement('canvas');
          const ctx = canvas.getContext('2d');
          const image = new Image();
          image.crossOrigin = 'anonymous';
          await new Promise((resolve, reject) => {
            image.onload = () => {
              canvas.width = image.naturalWidth;
              canvas.height = image.naturalHeight;
              ctx.drawImage(image, 0, 0);
              resolve();
            };
            image.onerror = reject;
            image.src = img.src;
          });
          const link = document.createElement('a');
          link.download = filename;
          link.href = canvas.toDataURL('image/png');
          document.body.appendChild(link);
          link.click();
          document.body.removeChild(link);
          console.log(`✅ 已下载(div转PNG): ${filename}`);
        } else {
          console.warn(`⚠️ 画板 ${i+1} 未找到图片资源，跳过`);
        }
      }

      // 防止浏览器拦截批量下载
      await new Promise(resolve => setTimeout(resolve, 500));
    } catch (err) {
      console.error(`❌ 画板 ${i+1} 下载失败:`, err);
    }
  }

  alert(`🎉 全部处理完成！成功下载 ${artboards.length} 张设计稿图片`);
})();
