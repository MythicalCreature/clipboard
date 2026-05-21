---
date: 2026-05-21T21:03:04+08:00
source: clipboard
chars: 876
---

let allQuestions = [];

// ======================
// 在这里配置你的通配符
// ======================
const WILDCARD = "言语理解与表达.json"; // 👈 只改这一行！

async function loadAllQuestions() {
  try {
    let all = [];
    let list = [];

    // 自动获取所有 json 文件列表
    try {
      const res = await fetch("filelist.json");
      list = await res.json();
    } catch (e) {}

    // 过滤：只加载 以 WILDCARD 结尾的文件
    const files = list.filter(f => f.endsWith(WILDCARD));

    // 批量加载
    const promises = files.map(f => fetch(f).then(r => r.json()));
    const results = await Promise.all(promises);

    // 合并所有题目
    all = results.flat();
    allQuestions = all;
    render();
  } catch (err) {
    console.error("加载失败", err);
  }
}

window.addEventListener("load", loadAllQuestions);
