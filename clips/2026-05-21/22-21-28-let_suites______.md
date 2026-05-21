---
date: 2026-05-21T22:21:28+08:00
source: clipboard
chars: 1677
---

let suites = [];
let allQuestions = [];

const STORE_KEY = "xsyy_verbal_suite_answers_v1";
let progress = JSON.parse(localStorage.getItem(STORE_KEY) || "{}");
let currentSuite = "all";
let reveal = false;

document.getElementById("loadBtn").addEventListener("click", async () => {
  try {
    const folderHandle = await window.showDirectoryPicker();
    const results = [];

    // 遍历文件夹所有 JSON
    for await (const entry of folderHandle.values()) {
      if (entry.kind === "file" && entry.name.endsWith(".json")) {
        try {
          const file = await entry.getFile();
          const text = await file.text();
          const data = JSON.parse(text);

          // 👇 这里自动兼容 2 种 JSON 格式
          let questions = [];
          let name = entry.name.replace(".json", "");

          if (Array.isArray(data)) {
            // 格式1：直接是 [{},{}]
            questions = data;
          } else if (data.questions) {
            // 格式2：{ questions: [...] }
            questions = data.questions;
            name = data.name || name;
          }

          results.push({
            name: name,
            count: questions.length,
            questions: questions
          });
        } catch (e) {}
      }
    }

    // 合并所有题目
    allQuestions = results.flatMap(item => item.questions);

    // 生成 suites
    suites = results.map((item, idx) => ({
      suiteId: idx + 1,
      suiteName: item.name,
      count: item.count
    }));

    alert("加载成功！共 " + suites.length + " 套题库");
    render();
  } catch (err) {
    console.error("错误：", err);
    alert("加载失败");
  }
});
