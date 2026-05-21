---
date: 2026-05-22T00:41:25+08:00
source: clipboard
chars: 831
---

// 在 initSuites 函数开头定义
let filteredSuites = [];

// 然后在 renderSuiteList 里更新它
function renderSuiteList() {
    const y = yearSelect?.value || "all";
    const a = areaSelect?.value || "all";

    // 筛选套题
    filteredSuites = suites.filter(s => {
        const name = s.name;
        const yearOk = y === "all" || name.includes(y);
        const areaOk = a === "all" || getAreaTag(name) === a;
        return yearOk && areaOk;
    });

    // ... 后面的套题下拉、侧边按钮更新逻辑不变 ...

    // 更新总数
    const filteredCount = filteredSuites.reduce((sum, s) => sum + s.questions.length, 0);
    document.getElementById("totalCount").innerText = filteredCount;

    // 重置为全部套题并渲染
    currentSuite = "all";
    suiteSelect.value = "all";
    render();
}
