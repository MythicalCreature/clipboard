---
date: 2026-05-22T00:44:38+08:00
source: clipboard
chars: 5638
---

  function initSuites() {
            let filteredSuites = suites; // 全局：筛选后的套题
            const yearSelect = document.getElementById("yearSelect");
            const areaSelect = document.getElementById("areaSelect");

            // 地区标签处理
            const getAreaTag = (name) => {
                if (/广东|县级|乡镇|选调/.test(name)) return "广东";
                if (/联考/.test(name)) return "联考";

                // 先去掉年份
                let area = name.replace(/^\d{4}\s*/, "");
                // 删掉所有科目名
                const subjects = ["言语理解与表达", "判断推理", "数量关系", "资料分析", "常识判断", "中级"];
                subjects.forEach(sub => {
                    area = area.replace(sub, "").trim();
                });
                // 删掉A/B后缀
                area = area.replace(/\s+[AB]$/, "").trim();
                return area || name;
            };

            // 1. 先提取所有基础数据
            const allYears = [...new Set(suites.map(s => {
                const m = s.name.match(/\d{4}/);
                return m ? m[0] : null;
            }).filter(Boolean))].sort((a, b) => b - a);

            const allAreas = [...new Set(suites.map(s => getAreaTag(s.name)).filter(Boolean))];

            // 2. 联动更新：年份下拉（根据选中的地区过滤）
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
                    // 保持原来的选中值，如果还在新列表里
                    if (availableYears.includes(currentValue)) {
                        yearSelect.value = currentValue;
                    } else {
                        yearSelect.value = "all";
                    }
                }
            }

            // 3. 联动更新：地区下拉（根据选中的年份过滤）
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
                    // 保持原来的选中值，如果还在新列表里
                    if (availableAreas.includes(currentValue)) {
                        areaSelect.value = currentValue;
                    } else {
                        areaSelect.value = "all";
                    }
                }
            }

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

            // 5. 初始渲染
            updateYearOptions("all");
            updateAreaOptions("all");
            renderSuiteList();

            // 6. 绑定联动事件
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
            // 初始加载时，默认是全部套题
            filteredSuites = suites;
        }

