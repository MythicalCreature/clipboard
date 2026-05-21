---
date: 2026-05-22T00:31:07+08:00
source: clipboard
chars: 473
---

const getAreaTag = (name) => {
    // 核心：所有广东相关 → 全部统一叫 广东
    if (/广东|县级|乡镇|选调/.test(name)) return "广东";
    // 所有联考相关 → 统一叫 联考
    if (/联考|A|B/.test(name)) return "联考";

    // 其他省份：去掉年份 + 去掉科目，只保留省份名字
    const noYear = name.replace(/^\d{4}\s*/, "");
    const match = noYear.match(/^[\u4e00-\u9fa5]+/);
    return match ? match[0] : null;
};
