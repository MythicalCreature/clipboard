---
date: 2026-05-22T00:14:40+08:00
source: clipboard
chars: 1427
---

    function initSuites() {
            // 下拉框：用 题目里的 suiteIndex 作为 value
            suiteSelect.innerHTML = '<option value="all">全部套题</option>' + suites.map((s) => {
                // 取这套题第一题的 suiteIndex
                const suiteIndex = s.questions[0]?.suiteIndex || 0;
                return `<option value="${suiteIndex}">${escapeHtml(s.name)}（${s.questions.length}）</option>`;
            }).join("");

            // 侧边按钮：用 题目里的 suiteIndex 作为 data-suite
            suiteList.innerHTML = suites.map((s) => {
                // 取这套题第一题的 suiteIndex
                const suiteIndex = s.questions[0]?.suiteIndex || 0;
                return `<button class="suite-btn" data-suite="${suiteIndex}">
            ${escapeHtml(s.name)} 
            <span class="suite-count">${s.questions.length}</span>
        </button>`;
            }).join("");

            // 点击事件
            document.querySelectorAll(".suite-btn").forEach(btn => {
                btn.addEventListener("click", () => {
                    currentSuite = btn.dataset.suite;
                    suiteSelect.value = currentSuite;
                    render();
                });
            });

            suiteSelect.addEventListener("change", () => {
                currentSuite = suiteSelect.value;
                render();
            });
        }

