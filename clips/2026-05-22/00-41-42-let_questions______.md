---
date: 2026-05-22T00:41:42+08:00
source: clipboard
chars: 409
---

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

