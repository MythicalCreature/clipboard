---
date: 2026-05-22T00:16:42+08:00
source: clipboard
chars: 2811
---

function initSuites() {
    // 自动提取所有 年份 + 省份
    const allYears = [...new Set(suites.map(s => s.name.match(/\d{4}/)?.[0]).filter(Boolean))].sort((a, b) => b - a);
    const allProvinces = [...new Set(suites.map(s => {
        const match = s.name.match(/(^|[^\d])([^0-9\s]+)/);
        return match ? match[2] : null;
    }).filter(Boolean))];

    // 年份下拉
    const yearSelect = document.getElementById("yearSelect");
    yearSelect.innerHTML = `
        <option value="all">全部年份</option>
        ${allYears.map(y => `<option value="${y}">${y}年</option>`).join("")}
    `;

    // 省份下拉
    const provinceSelect = document.getElementById("provinceSelect");
    provinceSelect.innerHTML = `
        <option value="all">全部省份</option>
        ${allProvinces.map(p => `<option value="${p}">${p}</option>`).join("")}
    `;

    // 渲染套题列表（根据 年份 + 省份 筛选）
    function renderSuiteList() {
        const y = yearSelect.value;
        const p = provinceSelect.value;

        const filtered = suites.filter(s => {
            const yearOk = y === "all" || s.name.includes(y);
            const provinceOk = p === "all" || s.name.includes(p);
            return yearOk && provinceOk;
        });

        // 下拉框
        suiteSelect.innerHTML = `
            <option value="all">全部套题</option>
            ${filtered.map(s => {
                const idx = s.questions[0]?.suiteIndex || 0;
                return `<option value="${idx}">${escapeHtml(s.name)}（${s.questions.length}题）</option>`;
            }).join("")}
        `;

        // 侧边按钮
        suiteList.innerHTML = filtered.map(s => {
            const idx = s.questions[0]?.suiteIndex || 0;
            return `
            <button class="suite-btn" data-suite="${idx}">
                ${escapeHtml(s.name)}
                <span class="suite-count">${s.questions.length}</span>
            </button>
            `;
        }).join("");

        // 重新绑定点击
        document.querySelectorAll(".suite-btn").forEach(btn => {
            btn.addEventListener("click", () => {
                currentSuite = btn.dataset.suite;
                suiteSelect.value = currentSuite;
                render();
            });
        });
    }

    // 初始渲染
    renderSuiteList();

    // 事件：年份/省份变化 → 自动刷新套题列表
    yearSelect.addEventListener("change", () => {
        currentSuite = "all";
        renderSuiteList();
        render();
    });

    provinceSelect.addEventListener("change", () => {
        currentSuite = "all";
        renderSuiteList();
        render();
    });

    suiteSelect.addEventListener("change", () => {
        currentSuite = suiteSelect.value;
        render();
    });
}
