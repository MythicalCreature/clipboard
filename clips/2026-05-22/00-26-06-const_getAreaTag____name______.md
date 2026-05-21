---
date: 2026-05-22T00:26:06+08:00
source: clipboard
chars: 522
---

const getAreaTag = (name) => {
    // 1. 广东/联考特殊规则保持不变
    if (/广东|县级|乡镇|选调|[一三]/.test(name)) return "广东";
    if (/联考|[AB]/.test(name)) return "联考";

    // 2. 匹配开头的省份/地区（只取汉字，自动跳过前面的年份数字）
    // 先把开头的年份去掉，再提取地名
    const noYearName = name.replace(/^\d{4}\s*/, "");
    const areaMatch = noYearName.match(/^[\u4e00-\u9fa5]+/);

    return areaMatch ? areaMatch[0].trim() : null;
};
