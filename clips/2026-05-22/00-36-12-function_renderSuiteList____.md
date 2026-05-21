---
date: 2026-05-22T00:36:12+08:00
source: clipboard
chars: 1697
---

function renderSuiteList() {
    const y = yearSelect?.value || "all";
    const a = areaSelect?.value || "all";

    // 筛选套题
    const filteredSuites = suites.filter(s => {
        const name = s.name;
        const yearOk = y === "all" || name.includes(y);
        const areaOk = a === "all" || getAreaTag(name) === a;
        return yearOk && areaOk;
    });

    // 更新套题下拉
    suiteSelect.innerHTML = `
        <option value="all">全部套题</option>
        ${filteredSuites.map(s => {
            const idx = s.questions[0]?.suiteIndex || 0;
            return `<option value="${idx}">${escapeHtml(s.name)}（${s.questions.length}题）</option>`;
        }).join("")}
    `;

    // 更新侧边按钮
    suiteList.innerHTML = filteredSuites.map(s => {
        const idx = s.questions[0]?.suiteIndex || 0;
        return `
        <button class="suite-btn" data-suite="${idx}">
            ${escapeHtml(s.name)}
            <span class="suite-count">${s.questions.length}</span>
        </button>
        `;
    }).join("");

    // 重新绑定按钮事件
    document.querySelectorAll(".suite-btn").forEach(btn => {
        btn.addEventListener("click", () => {
            currentSuite = btn.dataset.suite;
            suiteSelect.value = currentSuite;
            render();
        });
    });

    // ✅ 关键：更新「全部套题」总数
    const filteredCount = filteredSuites.reduce((sum, s) => sum + s.questions.length, 0);
    document.getElementById("totalCount").innerText = filteredCount;

    // ✅ 关键：筛选后自动重置为“全部套题”并重新渲染题目
    currentSuite = "all";
    suiteSelect.value = "all";
    render();
}
