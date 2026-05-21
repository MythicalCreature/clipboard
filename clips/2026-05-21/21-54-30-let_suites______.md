---
date: 2026-05-21T21:54:30+08:00
source: clipboard
chars: 1319
---

let suites = [];
let allQuestions = [];
const STORE_KEY = "xsyy_verbal_suite_answers_v1";
let progress = JSON.parse(localStorage.getItem(STORE_KEY) || "{}");
let currentSuite = "all";
let reveal = false;

// 页面加载时自动读取 files.json 并加载所有题库
async function initFromFilesJson() {
  try {
    // 1. 读取文件列表
    const resp = await fetch("files.json");
    const fileList = await resp.json();

    // 2. 只保留 .json 文件
    const jsonFiles = fileList.filter(name => name.endsWith(".json"));

    // 3. 并行加载所有题库
    const promises = jsonFiles.map(name =>
      fetch(name).then(r => r.json())
    );
    const results = await Promise.all(promises);

    // 4. 合并所有题目
    allQuestions = results.flatMap(item => item.questions || []);

    // 5. 自动生成 suites 数组
    suites = jsonFiles.map((name, index) => {
      const data = results[index];
      return {
        suiteId: index + 1,
        suiteName: data.name || name.replace(".json", ""),
        count: data.count || (data.questions?.length || 0)
      };
    });

    // 加载完成后渲染页面
    render();
  } catch (err) {
    console.error("从 files.json 加载题库失败：", err);
  }
}

// 页面加载时自动执行
window.addEventListener("load", initFromFilesJson);
