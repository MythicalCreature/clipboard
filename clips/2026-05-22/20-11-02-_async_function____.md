---
date: 2026-05-22T20:11:02+08:00
source: clipboard
chars: 2436
---

(async function() {
  console.log('🚀 开始从网络请求批量导出摹客图片为PNG...');

  // 1. 从性能面板的请求中，筛选出摹客的设计稿图片
  // 这里直接用所有带mockplus域名、且是图片格式的请求
  const requests = window.performance.getEntriesByType('resource');
  const imageUrls = [...new Set(
    requests
      .filter(req => 
        (req.name.includes('mockplus') || req.name.includes('app.mockplus')) && 
        (req.name.endsWith('.png') || req.name.endsWith('.webp') || req.name.includes('image'))
      )
      .map(req => req.name)
  )];

  console.log(`📋 找到 ${imageUrls.length} 张图片请求`);

  if (imageUrls.length === 0) {
    alert('未找到图片请求，请先刷新页面并手动滚动加载所有设计稿');
    return;
  }

  // 2. 逐个下载并转换为PNG
  for (let i = 0; i < imageUrls.length; i++) {
    const url = imageUrls[i];
    const filename = `mockplus_design_${String(i+1).padStart(3, '0')}.png`;

    try {
      // 创建canvas，将webp/png转为标准PNG
      const canvas = document.createElement('canvas');
      const ctx = canvas.getContext('2d');
      const img = new Image();
      img.crossOrigin = 'anonymous'; // 解决跨域问题

      await new Promise((resolve, reject) => {
        img.onload = () => {
          canvas.width = img.naturalWidth;
          canvas.height = img.naturalHeight;
          ctx.drawImage(img, 0, 0);
          resolve();
        };
        img.onerror = (err) => {
          console.warn(`⚠️ 图片加载失败: ${url}`, err);
          resolve(); // 跳过失败的图片，继续下一个
        };
        img.src = url;
      });

      // 下载PNG
      if (canvas.width > 0 && canvas.height > 0) {
        const link = document.createElement('a');
        link.download = filename;
        link.href = canvas.toDataURL('image/png');
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        console.log(`✅ 已下载: ${filename}`);
      } else {
        console.warn(`⚠️ 图片无有效尺寸，跳过: ${url}`);
      }

      // 防止浏览器拦截批量下载
      await new Promise(resolve => setTimeout(resolve, 300));
    } catch (err) {
      console.error(`❌ 下载失败: ${url}`, err);
    }
  }

  alert(`🎉 全部处理完成！共处理 ${imageUrls.length} 张图片，成功下载！`);
})();
