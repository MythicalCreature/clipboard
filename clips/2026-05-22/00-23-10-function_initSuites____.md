---
date: 2026-05-22T00:23:10+08:00
source: clipboard
chars: 2864
---

function initSuites() {
    // 自动提取所有 年份
    const allYears = [...new Set(suites.map(s => {
        const m = s.name.match(/\d{4}/);
        return m ? m[0] : null;
    }).filter(Boolean))].sort((a, b) => b - a);

    // 地区标签处理：只有广东、联考特殊归类，其他原样取
    const getAreaTag = (name) => {
        if (/广东|县级|乡镇|选调|[一三]/.test(name)) return "广东";
        if (/联考|[AB]/.test(name)) return "联考";
        const match = name.match(/[\u4e00-\u9fa5a-zA-Z]+/);
        return match ? match[0] : null;
    };
    const allAreas = [...new Set(suites.map(s => getAreaTag(s.name)).filter(Boolean))];

    const yearSelect = document.getElementById("yearSelect");
    const areaSelect = document.getElementById("areaSelect");

    yearSelect.innerHTML = `
        <option value="all">全部年份</option>
        ${allYears.map(y => `<option value="${y}">${y}年</option>`).join("")}
    `;

    areaSelect.innerHTML = `
        <option value="all">全部地区</option>
        ${allAreas.map(a => `<option value="${a}">${a}</option>`).join("")}
    `;

    function renderSuiteList() {
        const y = yearSelect.value;
        const a = areaSelect.value;

        const filtered = suites.filter(s => {
            const name = s.name;
            const yearOk = y === "all" || name.includes(y);
            const areaOk = a === "all" || getAreaTag(name) === a;
            return yearOk && areaOk;
        });

        suiteSelect.innerHTML = `
            <option value="all">全部套题</option>
            ${filtered.map(s => {
                const idx = s.questions[0]?.suiteIndex || 0;
                return `<option value="${idx}">${escapeHtml(s.name)}（${s.questions.length}题）</option>`;
            }).join("")}
        `;

        suiteList.innerHTML = filtered.map(s => {
            const idx = s.questions[0]?.suiteIndex || 0;
            return `
            <button class="suite-btn" data-suite="${idx}">
                ${escapeHtml(s.name)}
                <span class="suite-count">${s.questions.length}</span>
            </button>
            `;
        }).join("");

        document.querySelectorAll(".suite-btn").forEach(btn => {
            btn.addEventListener("click", () => {
                currentSuite = btn.dataset.suite;
                suiteSelect.value = currentSuite;
                render();
            });
        });
    }

    renderSuiteList();

    yearSelect.addEventListener("change", () => {
        currentSuite = "all";
        renderSuiteList();
        render();
    });

    areaSelect.addEventListener("change", () => {
        currentSuite = "all";
        renderSuiteList();
        render();
    });

    suiteSelect.addEventListener("change", () => {
        currentSuite = suiteSelect.value;
        render();
    });
}
