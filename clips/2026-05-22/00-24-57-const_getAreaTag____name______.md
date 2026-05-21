---
date: 2026-05-22T00:24:57+08:00
source: clipboard
chars: 535
---

const getAreaTag = (name) => {
    // 广东归类
    if (/广东|县级|乡镇|选调|[一三]/.test(name)) return "广东";
    // 联考归类
    if (/联考|[AB]/.test(name)) return "联考";
    // 提取纯省市地名，过滤科目
    const areaMatch = name.match(/^(.*?)[\u4e00-\u9fa5]{2,}(?=言语|判断|数量|资料|常识|中级)/);
    if(areaMatch) return areaMatch[1].trim();
    // 兜底提取开头地域
    const normalMatch = name.match(/^[\u4e00-\u9fa5]+/);
    return normalMatch ? normalMatch[0] : null;
};
