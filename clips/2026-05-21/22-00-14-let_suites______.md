---
date: 2026-05-21T22:00:14+08:00
source: clipboard
chars: 1677
---

let suites = [];
let allQuestions = [];
const STORE_KEY = "xsyy_verbal_suite_answers_v1";
let progress = JSON.parse(localStorage.getItem(STORE_KEY) || "{}");
let currentSuite = "all";
let reveal = false;

// =============================================
// 🔥 全自动：选择文件夹 → 自动读所有JSON
// =============================================
async function autoLoadAllJson() {
  try {
    alert("请选择你的题库文件夹！\n（就是放bbb.html和所有json的文件夹）");
    
    // 让你选择文件夹
    const folderHandle = await window.showDirectoryPicker();
    const jsonFiles = [];
    const fileHandles = [];

    // 自动扫描所有 .json 文件
    for await (const entry of folderHandle.values()) {
      if (entry.kind === "file" && entry.name.endsWith(".json") && !entry.name.includes("files.json")) {
        jsonFiles.push(entry.name);
        fileHandles.push(entry);
      }
    }

    // 读取所有 JSON 内容
    const results = [];
    for (const handle of fileHandles) {
      const file = await handle.getFile();
      const text = await file.text();
      const data = JSON.parse(text);
      results.push(data);
    }

    // 合并所有题目
    allQuestions = results.flatMap(item => item.questions || []);

    // 自动生成 suites ✅
    suites = results.map((data, index) => ({
      suiteId: index + 1,
      suiteName: data.name,
      count: data.count
    }));

    alert("加载成功！共 " + suites.length + " 套题库");
    render();

  } catch (err) {
    console.error("加载失败", err);
    alert("加载失败，请重试！");
  }
}

window.addEventListener("load", autoLoadAllJson);
