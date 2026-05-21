---
date: 2026-05-21T22:23:37+08:00
source: clipboard
chars: 2100
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

    for await (const entry of folderHandle.values()) {
      if (entry.kind === "file" && entry.name.endsWith(".json")) {
        try {
          const file = await entry.getFile();
          const text = await file.text();
          const data = JSON.parse(text);

          let questions = [];
          let name = entry.name.replace(".json", "");

          // 👇 自动兼容两种格式
          if (Array.isArray(data)) {
            questions = data;
          } else if (data.questions && Array.isArray(data.questions)) {
            questions = data.questions;
            name = data.name || name;
          }

          // 👇 强制保证题目结构完整（关键！不报错！）
          const validQuestions = questions.map(q => ({
            id: q.id || Math.random().toString(36),
            suiteName: q.suiteName || name,
            num: q.num || 0,
            stem: q.stem || "",
            options: q.options || [],
            answer: q.answer || "",
            analysis: q.analysis || ""
          }));

          results.push({
            name: name,
            count: validQuestions.length,
            questions: validQuestions
          });
        } catch (e) {}
      }
    }

    // 合并
    allQuestions = results.flatMap(r => r.questions);
    console.log("最终题目总数", allQuestions.length);

    // 生成 suites
    suites = results.map((item, idx) => ({
      suiteId: idx + 1,
      suiteName: item.name,
      count: item.count
    }));

    alert("加载成功！题库：" + suites.length + " 套，题目：" + allQuestions.length);
    render();
  } catch (err) {
    console.error("最终错误：", err);
    alert("加载出错：" + err.message);
  }
});
