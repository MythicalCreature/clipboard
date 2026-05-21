---
date: 2026-05-21T22:31:03+08:00
source: clipboard
chars: 1801
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
    const suiteList = [];

    // 遍历所有 JSON
    for await (const entry of folderHandle.values()) {
      if (entry.kind === "file" && entry.name.endsWith(".json")) {
        try {
          const file = await entry.getFile();
          const text = await file.text();
          const data = JSON.parse(text);

          // ==========================================
          // 只处理你有的 2 种格式
          // ==========================================
          if (Array.isArray(data)) {
            // 格式1：[ {name, question}, {name, question} ]
            for (const suite of data) {
              suiteList.push({
                name: suite.name || "未命名",
                questions: suite.question || []
              });
            }
          } else {
            // 格式2：{ name, question }
            suiteList.push({
              name: data.name || "未命名",
              questions: data.question || []
            });
          }
        } catch (e) {}
      }
    }

    // 合并所有题目
    allQuestions = suiteList.flatMap(item => item.questions);

    // 生成 suites
    suites = suiteList.map((item, idx) => ({
      suiteId: idx + 1,
      suiteName: item.name,
      count: item.questions.length
    }));

    alert("加载成功！\n题库：" + suites.length + " 套\n题目：" + allQuestions.length);
    render();
  } catch (err) {
    console.error("错误：", err);
  }
});
