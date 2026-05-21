---
date: 2026-05-21T22:02:14+08:00
source: clipboard
chars: 1164
---

let suites = [];
let allQuestions = [];
const STORE_KEY = "xsyy_verbal_suite_answers_v1";
let progress = JSON.parse(localStorage.getItem(STORE_KEY) || "{}");
let currentSuite = "all";
let reveal = false;

// 点击按钮才加载 → 解决安全报错
document.getElementById("loadBtn").addEventListener("click", async () => {
  try {
    const folderHandle = await window.showDirectoryPicker();
    const results = [];

    // 遍历文件夹所有 JSON
    for await (const entry of folderHandle.values()) {
      if (entry.kind === "file" && entry.name.endsWith(".json")) {
        const file = await entry.getFile();
        const text = await file.text();
        const data = JSON.parse(text);
        results.push(data);
      }
    }

    // 合并所有题目
    allQuestions = results.flatMap(item => item.questions || []);

    // 自动生成 suites
    suites = results.map((data, index) => ({
      suiteId: index + 1,
      suiteName: data.name,
      count: data.count
    }));

    alert("加载成功！题库数量：" + suites.length);
    render();
  } catch (err) {
    console.error("加载失败", err);
    alert("加载失败");
  }
});
