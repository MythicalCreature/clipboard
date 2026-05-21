---
date: 2026-05-22T00:43:54+08:00
source: clipboard
chars: 592
---

function filteredQuestions() {
    // 👇 直接用筛选后的题目
    let qs = window.__currentFilteredQuestions || [];

    const filter = document.getElementById("filter").value;
    if (filter === "wrong") {
        qs = qs.filter(q => getUserAnswer(q.id) && !isCorrect(q));
    } else if (filter === "correct") {
        qs = qs.filter(q => getUserAnswer(q.id) && isCorrect(q));
    } else if (filter === "unanswered") {
        qs = qs.filter(q => !getUserAnswer(q.id));
    } else if (filter === "doubt") {
        qs = qs.filter(q => progress[q.id]?.doubt);
    }
    return qs;
}
