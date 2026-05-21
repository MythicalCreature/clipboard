---
date: 2026-05-22T00:43:16+08:00
source: clipboard
chars: 1890
---

function render() {
    // 👇 【核心修复】从筛选后的套题里拿题目，不是从全部suites拿
    let allQuestions = [];

    if (currentSuite === "all") {
        // 全部套题 = 筛选后的所有套题
        allQuestions = filteredSuites.flatMap(s => s.questions);
    } else {
        // 单个套题 = 从筛选后的套题里找
        const suite = filteredSuites.find(s => s.questions[0]?.suiteIndex == currentSuite);
        allQuestions = suite ? suite.questions : [];
    }

    // 👇 把筛选后的题目全局覆盖，让 filteredQuestions 能读到！
    window.__currentFilteredQuestions = allQuestions;

    const filter = document.getElementById("filter").value;

    if (filter === "wrong") {
        if (window.lastFilter !== filter) {
            reveal = true;
        }
    }
    window.lastFilter = filter;

    document.querySelectorAll(".suite-btn").forEach(btn => btn.classList.toggle("active", btn.dataset.suite === String(currentSuite)));
    suiteSelect.value = currentSuite;

    // 👇 这里会自动使用筛选后的题目
    const list = filteredQuestions();

    let done = 0, correct = 0, wrong = 0, doubt = 0;
    list.forEach(q => {
        const ua = getUserAnswer(q.id);
        const ok = isCorrect(q);
        if (ua) done++;
        if (ok === true) correct++;
        if (ok === false) wrong++;
        if (progress[q.id]?.doubt) doubt++;
    });

    document.getElementById("statTotal").textContent = list.length;
    document.getElementById("statDone").textContent = done;
    document.getElementById("statCorrect").textContent = correct;
    document.getElementById("statWrong").textContent = wrong;
    document.getElementById("statDoubt").textContent = doubt;

    questionsEl.innerHTML = list.map(renderQuestion).join("") || '<div class="card">没有符合条件的题目。</div>';
    bindQuestionEvents();
}
