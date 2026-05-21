---
date: 2026-05-22T00:33:08+08:00
source: clipboard
chars: 687
---

const getAreaTag = (name) => {
    // 1. 广东/联考 特殊规则不变
    if (/广东|县级|乡镇|选调/.test(name)) return "广东";
    if (/联考/.test(name)) return "联考";

    // 2. 先把所有年份去掉
    let area = name.replace(/^\d{4}\s*/, "");

    // 3. 把所有科目名称全部删掉
    const subjects = ["言语理解与表达", "判断推理", "数量关系", "资料分析", "常识判断", "中级"];
    subjects.forEach(sub => {
        area = area.replace(sub, "").trim();
    });

    // 4. 再把A/B也删掉
    area = area.replace(/\s+[AB]$/, "").trim();

    // 5. 兜底：如果还是空的，就用原来的名字
    return area || name;
};
