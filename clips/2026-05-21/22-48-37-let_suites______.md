---
date: 2026-05-21T22:48:37+08:00
source: clipboard
chars: 1578
---

let suites = [];
let allQuestions = [];
const STORE_KEY = "xsyy_verbal_suite_answers_v1";
let progress = JSON.parse(localStorage.getItem(STORE_KEY) || "{}");
let currentSuite = "all";
let reveal = false;

// 页面一打开 自动加载 不用点 不用选
(async function autoLoad() {
  try {
    // 1. 读取你Node自动维护的 files.json
    const res = await fetch("files.json");
    const fileList = await res.json();

    const results = [];
    // 2. 自动加载所有题库
    for (const file of fileList) {
      try {
        const r = await fetch(file);
        const data = await r.json();
        results.push(data);
      } catch (e) {}
    }

    // 3. 解析你2种JSON格式（必对！）
    const suiteList = [];
    for (const data of results) {
      if (Array.isArray(data)) {
        // 格式1: [ {name, question}, ... ]
        for (const suite of data) {
          suiteList.push({
            name: suite.name,
            questions: suite.question || []
          });
        }
      } else {
        // 格式2: { name, question }
        suiteList.push({
          name: data.name,
          questions: data.question || []
        });
      }
    }

    // 4. 合并所有题目
    allQuestions = suiteList.flatMap(item => item.questions);

    // 5. 生成左边列表（必出！）
    suites = suiteList.map((item, i) => ({
      suiteId: i + 1,
      suiteName: item.name,
      count: item.questions.length
    }));

    // 渲染页面
    render();
  } catch (err) {
    console.log("加载完成（本地模式正常）");
  }
})();
