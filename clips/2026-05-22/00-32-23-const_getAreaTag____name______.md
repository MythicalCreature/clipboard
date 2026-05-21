---
date: 2026-05-22T00:32:23+08:00
source: clipboard
chars: 990
---

const getAreaTag = (name) => {
    // 1. 广东相关（含县级/乡镇/选调）统一归类为广东
    if (/广东|县级|乡镇|选调/.test(name)) {
        return "广东";
    }

    // 2. 联考相关（含A/B）统一归类为联考
    if (/联考/.test(name)) {
        return "联考";
    }

    // 3. 其他省份：去掉年份、去掉后面的科目文字，只保留省份名
    // 先把开头的年份去掉
    const nameWithoutYear = name.replace(/^\d{4}\s*/, "");

    // 匹配省份名（只取开头的汉字，遇到“言语/判断/数量/资料/常识/中级/A/B”就停止）
    const match = nameWithoutYear.match(/^[\u4e00-\u9fa5]+(?=\s*(言语|判断|数量|资料|常识|中级|A|B|$))/);

    if (match) {
        return match[0].trim();
    }

    // 兜底：直接取开头的省份名（防止正则匹配失败）
    const fallbackMatch = nameWithoutYear.match(/^[\u4e00-\u9fa5]+/);
    return fallbackMatch ? fallbackMatch[0].trim() : null;
};
