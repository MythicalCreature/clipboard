---
date: 2026-05-22T00:30:55+08:00
source: clipboard
chars: 4496
---

function initSuites() {
    const yearSelect = document.getElementById("yearSelect");
    const areaSelect = document.getElementById("areaSelect");

    // 1. 提取年份（用于筛选）
    const allYears = [...new Set(suites.map(s => {
        const m = s.name.match(/\d{4}/);
        return m ? m[0] : null;
    }).filter(Boolean))].sort((a, b) => b - a);

    // 2. 地区标签处理：
    // - 广东、联考保留特殊归类，但县级/乡镇会被区分
    // - 其他省份自动剥离科目名，只保留省份
    const getAreaTag = (name) => {
        // 联考特殊规则
        if (/联考/.test(name)) return "联考";
        // 广东规则：县级/乡镇/选调/广东，都保留，但县级/乡镇会被区分
        if (/广东县级/.test(name)) return "广东县级";
        if (/广东乡镇/.test(name)) return "广东乡镇";
        if (/广东选调/.test(name)) return "广东选调";
        if (/广东/.test(name)) return "广东";

        // 其他省份：去掉年份、去掉科目，只保留省份
        const noYearName = name.replace(/^\d{4}\s*/, "");
        // 匹配科目名并剔除
        const areaMatch = noYearName.match(/^[\u4e00-\u9fa5]+(?=\s*(言语|判断|数量|资料|常识|中级|A|B))/);
        if (areaMatch) return areaMatch[0].trim();
        // 兜底：直接取开头的省份名
        const normalMatch = noYearName.match(/^[\u4e00-\u9fa5]+/);
        return normalMatch ? normalMatch[0].trim() : null;
    };

    // 3. 提取所有地区标签（过滤掉空值和年份）
    const allAreas = [...new Set(
        suites.map(s => getAreaTag(s.name))
            .filter(tag => tag && !/^\d{4}$/.test(tag))
    )];

    // 4. 渲染年份下拉
    if (yearSelect) {
        yearSelect.innerHTML = `
            <option value="all">全部年份</option>
            ${allYears.map(y => `<option value="${y}">${y}年</option>`).join("")}
        `;
    }

    // 5. 渲染地区下拉
    if (areaSelect) {
        areaSelect.innerHTML = `
            <option value="all">全部地区</option>
            ${allAreas.map(a => `<option value="${a}">${a}</option>`).join("")}
        `;
    }

    // 6. 渲染套题列表 + 更新总数
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

        // ✅ 关键修复：更新「全部套题」旁边的总数
        const filteredCount = filteredSuites.reduce((sum, s) => sum + s.questions.length, 0);
        document.getElementById("totalCount").innerText = filteredCount;
    }

    // 初始渲染
    renderSuiteList();

    // 绑定筛选事件
    if (yearSelect) {
        yearSelect.addEventListener("change", () => {
            currentSuite = "all";
            renderSuiteList();
            render();
        });
    }

    if (areaSelect) {
        areaSelect.addEventListener("change", () => {
            currentSuite = "all";
            renderSuiteList();
            render();
        });
    }

    suiteSelect.addEventListener("change", () => {
        currentSuite = suiteSelect.value;
        render();
    });
}
