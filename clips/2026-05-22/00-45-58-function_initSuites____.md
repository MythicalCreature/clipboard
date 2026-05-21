---
date: 2026-05-22T00:45:58+08:00
source: clipboard
chars: 5137
---

function initSuites() {
    const yearSelect = document.getElementById("yearSelect");
    const areaSelect = document.getElementById("areaSelect");

    // 地区标签处理
    const getAreaTag = (name) => {
        if (/广东|县级|乡镇|选调/.test(name)) return "广东";
        if (/联考/.test(name)) return "联考";

        let area = name.replace(/^\d{4}\s*/, "");
        const subjects = ["言语理解与表达", "判断推理", "数量关系", "资料分析", "常识判断", "中级"];
        subjects.forEach(sub => {
            area = area.replace(sub, "").trim();
        });
        area = area.replace(/\s+[AB]$/, "").trim();
        return area || name;
    };

    // 提取年份
    const allYears = [...new Set(suites.map(s => {
        const m = s.name.match(/\d{4}/);
        return m ? m[0] : null;
    }).filter(Boolean))].sort((a, b) => b - a);

    // 提取地区
    const allAreas = [...new Set(suites.map(s => getAreaTag(s.name)).filter(Boolean))];

    // 更新年份下拉
    function updateYearOptions(selectedArea) {
        let availableYears = allYears;
        if (selectedArea && selectedArea !== "all") {
            availableYears = [...new Set(
                suites.filter(s => getAreaTag(s.name) === selectedArea)
                    .map(s => s.name.match(/\d{4}/)?.[0])
                    .filter(Boolean)
            )].sort((a, b) => b - a);
        }

        if (yearSelect) {
            const currentValue = yearSelect.value;
            yearSelect.innerHTML = `
                <option value="all">全部年份</option>
                ${availableYears.map(y => `<option value="${y}">${y}年</option>`).join("")}
            `;
            if (availableYears.includes(currentValue)) {
                yearSelect.value = currentValue;
            } else {
                yearSelect.value = "all";
            }
        }
    }

    // 更新地区下拉
    function updateAreaOptions(selectedYear) {
        let availableAreas = allAreas;
        if (selectedYear && selectedYear !== "all") {
            availableAreas = [...new Set(
                suites.filter(s => s.name.includes(selectedYear))
                    .map(s => getAreaTag(s.name))
                    .filter(Boolean)
            )];
        }

        if (areaSelect) {
            const currentValue = areaSelect.value;
            areaSelect.innerHTML = `
                <option value="all">全部地区</option>
                ${availableAreas.map(a => `<option value="${a}">${a}</option>`).join("")}
            `;
            if (availableAreas.includes(currentValue)) {
                areaSelect.value = currentValue;
            } else {
                areaSelect.value = "all";
            }
        }
    }

    // 渲染套题列表
    function renderSuiteList() {
        const y = yearSelect?.value || "all";
        const a = areaSelect?.value || "all";

        // ✅ 全局变量赋值
        filteredSuites = suites.filter(s => {
            const name = s.name;
            const yearOk = y === "all" || name.includes(y);
            const areaOk = a === "all" || getAreaTag(name) === a;
            return yearOk && areaOk;
        });

        // 套题下拉
        suiteSelect.innerHTML = `
            <option value="all">全部套题</option>
            ${filteredSuites.map(s => {
                const idx = s.questions[0]?.suiteIndex || 0;
                return `<option value="${idx}">${escapeHtml(s.name)}（${s.questions.length}题）</option>`;
            }).join("")}
        `;

        // 侧边按钮
        suiteList.innerHTML = filteredSuites.map(s => {
            const idx = s.questions[0]?.suiteIndex || 0;
            return `
            <button class="suite-btn" data-suite="${idx}">
                ${escapeHtml(s.name)}
                <span class="suite-count">${s.questions.length}</span>
            </button>
            `;
        }).join("");

        // 绑定事件
        document.querySelectorAll(".suite-btn").forEach(btn => {
            btn.addEventListener("click", () => {
                currentSuite = btn.dataset.suite;
                suiteSelect.value = currentSuite;
                render();
            });
        });

        // 更新总数
        const filteredCount = filteredSuites.reduce((sum, s) => sum + s.questions.length, 0);
        document.getElementById("totalCount").innerText = filteredCount;

        // 自动渲染题目
        currentSuite = "all";
        suiteSelect.value = "all";
        render();
    }

    // 初始
    updateYearOptions("all");
    updateAreaOptions("all");
    renderSuiteList();

    // 事件
    if (yearSelect) {
        yearSelect.addEventListener("change", () => {
            updateAreaOptions(yearSelect.value);
            renderSuiteList();
        });
    }

    if (areaSelect) {
        areaSelect.addEventListener("change", () => {
            updateYearOptions(areaSelect.value);
            renderSuiteList();
        });
    }

    suiteSelect.addEventListener("change", () => {
        currentSuite = suiteSelect.value;
        render();
    });
}
