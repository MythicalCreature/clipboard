---
date: 2026-05-21T21:02:05+08:00
source: clipboard
chars: 787
---

let allQuestions = [];

// 🔥 自动加载所有数字命名的 JSON：1.json、2.json、3.json ... 自动读到没有为止
async function loadAllQuestions() {
  try {
    let questions = [];
    let index = 1;

    // 循环加载，直到文件不存在为止
    while (true) {
      try {
        const res = await fetch(`${index}.json`);
        if (!res.ok) break; // 文件不存在就停止
        const data = await res.json();
        questions = questions.concat(data);
        index++;
      } catch (e) {
        break;
      }
    }

    allQuestions = questions;
    render(); // 加载完成自动渲染
  } catch (err) {
    console.error("加载题库失败：", err);
  }
}

// 页面加载自动读取所有 JSON
window.addEventListener("load", loadAllQuestions);
