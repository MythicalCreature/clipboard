---
date: 2026-05-22T00:42:04+08:00
source: clipboard
chars: 2301
---

     function render() {
            let questions = [];

            if (currentSuite === "all") {
                // 用筛选后的套题列表，而不是全部suites
                questions = filteredSuites.flatMap(s => s.questions);
            } else {
                // 按 suiteIndex 找对应的套题
                const suite = filteredSuites.find(s => s.questions[0]?.suiteIndex == currentSuite);
                if (suite) {
                    questions = suite.questions;
                }
            }

            const filter = document.getElementById("filter").value;

            // 👇 👇 👇 最终完美逻辑
            if (filter === "wrong") {
                // 只有【刚刚切换筛选】时才自动展开
                // 手动点过隐藏的，不强制覆盖
                if (window.lastFilter !== filter) {
                    reveal = true;
                }
            }
            // 记录上一次的筛选状态
            window.lastFilter = filter;

            document.querySelectorAll(".suite-btn").forEach(btn => btn.classList.toggle("active", btn.dataset.suite === String(currentSuite)));
            suiteSelect.value = currentSuite;
            const list = filteredQuestions();
            let done = 0
                , correct = 0
                , wrong = 0
                , doubt = 0;
            list.forEach(q => {
                const ua = getUserAnswer(q.id);
                const ok = isCorrect(q);
                if (ua)
                    done++;
                if (ok === true)
                    correct++;
                if (ok === false)
                    wrong++;
                if (progress[q.id]?.doubt)
                    doubt++;
            }
            );
            document.getElementById("statTotal").textContent = list.length;
            document.getElementById("statDone").textContent = done;
            document.getElementById("statCorrect").textContent = correct;
            document.getElementById("statWrong").textContent = wrong;
            document.getElementById("statDoubt").textContent = doubt;
            questionsEl.innerHTML = list.map(renderQuestion).join("") || '<div class="card">没有符合条件的题目。</div>';
            bindQuestionEvents();
        }

   
