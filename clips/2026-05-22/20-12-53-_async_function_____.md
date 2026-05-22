---
date: 2026-05-22T20:12:53+08:00
source: clipboard
chars: 389
---

(async function () {
  const canvas = document.querySelector("canvas");
  if (!canvas) {
    alert("未找到设计稿画布，请确保页面显示设计稿");
    return;
  }

  const link = document.createElement("a");
  link.download = "mockplus-all.png";
  link.href = canvas.toDataURL("image/png");
  link.click();
  alert("✅ 导出成功！文件名为：mockplus-all.png");
})();
