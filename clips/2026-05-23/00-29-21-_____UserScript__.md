---
date: 2026-05-23T00:29:21+08:00
source: clipboard
chars: 197756
---

// ==UserScript==
// @name         粉笔题库高效刷题辅助工具！
// @namespace    http://tampermonkey.net/
// @version      6.1
// @description  新增题型判断，前置判断题、单选题、多选题，修复单选题选择问题。清空收藏也支持按照类别。对所有练习进行修复，分成所有练习和所有试卷。增加粉笔解析跳转。新增兼容考试类型为行测和职测。新增来源、易错项、正确答案、全站准确率数据。支持试卷精准搜索与模糊筛选，可按正确率范围、模块类型快速定位题目，轻松收藏重点考题。提供灵活导出功能，可选择导出全部题目解析或仅导出错题，助力针对性复习。新增试卷单页下载与批量下载，一键保存学习资料。优化收藏管理，支持一键清空所有收藏，操作更便捷。全面覆盖各类练习场景，包括AI刷题班、7+1特训、粉刷刷专项及大笔筒练习，无论完成与否均可一键获取，让刷题效率翻倍，备考更轻松！
// @author       Mythical Creature
// @match        https://*.fenbi.com/*
// @connect      tiku.fenbi.com
// @connect      ke.fenbi.com
// @connect      fbstatic.cn
// @connect      cdn.jsdelivr.net
// @connect      cdnjs.cloudflare.com
// @grant        unsafeWindow
// @grant        GM_addStyle
// @grant        GM_xmlhttpRequest
// @grant        GM_setValue
// @grant        GM_getValue
// @grant        GM_xmlhttpRequest
// @grant        GM_download
// @require      https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js
// @require      https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js
// @require      https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.1.1/jspdf.umd.min.js
// ==/UserScript==

// 引入外部样式，定义工具的UI样式
GM_addStyle(`
   .paper-tool-container {
        position: fixed;          /* 固定定位，悬浮在页面上 */
        top: 20px;               /* 距离顶部20px */
        right: 20px;             /* 距离右侧20px */
        z-index: 9999;           /* 层级最高，确保不被其他元素遮挡 */
        background: white;       /* 白色背景 */
        border-radius: 8px;      /* 圆角边框 */
        box-shadow: 0 2px 10px rgba(0,0,0,0.2); /* 阴影效果 */
        width: 500px;            /* 宽度500px */
        max-height: calc(100vh - 40px); /* 最大高度为视口高度减去40px */
        display: flex;           /* 使用flex布局 */
        flex-direction: column;  /* 垂直方向排列 */
        transition: transform 0.3s ease; /* 变换过渡动画 */
    }
    /* 隐藏状态样式 */
    .paper-tool-container.hidden {
        transform: translateX(calc(100% - 40px)); /* 向右移动，只露出40px宽度 */
    }

    /* 隐藏状态下不显示内容区域 */
    .paper-tool-container.hidden .tool-content,
    .paper-tool-container.hidden .collect-actions,
    .paper-tool-container.hidden .log-area,
    .paper-tool-container.hidden .accuracy-filter,
    .paper-tool-container.hidden .tool-title,
    .paper-tool-container.hidden .search-container,
    .paper-tool-container.hidden .batch-download-container,
     .paper-tool-container.hidden .exam-type-container{
        display: none;
    }

    /* 隐藏状态下不显示头部边框 */
    .paper-tool-container.hidden .tool-header {
        border-bottom: none;
    }

    .exam-type-container {
        padding: 10px 15px;
        border-bottom: 1px solid #eee;
        display: flex;
        align-items: center;
        gap: 10px;
    }

    /* 搜索框样式 */
    .search-container {
        padding: 10px 15px;
        border-bottom: 1px solid #eee;
        display: flex;
        align-items: center;
        gap: 10px;
    }

    .search-input {
        flex: 1;
        padding: 6px 10px;
        border: 1px solid #ddd;
        border-radius: 4px;
        font-size: 14px;
        outline: none;
        transition: border-color 0.2s;
    }

    .search-input:focus {
        border-color: #1890ff;
    }

    .search-btn {
        padding: 6px 12px;
        background-color: #1890ff;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-size: 14px;
        transition: background-color 0.2s;
    }

    .search-btn:hover {
        background-color: #096dd9;
    }

    .search-btn.reset-btn {
        background-color: #f5f5f5;
        color: #666;
    }

    .search-btn.reset-btn:hover {
        background-color: #e5e5e5;
    }

    /* 批量下载选项样式 */
    .batch-download-container {
        padding: 10px 15px;
        border-bottom: 1px solid #eee;
        display: flex;
        align-items: center;
        gap: 10px;
    }

    .batch-download-label {
        font-size: 13px;
        color: #666;
    }

    .batch-download-pages {
        padding: 4px 8px;
        border: 1px solid #ddd;
        border-radius: 4px;
        font-size: 13px;
        width: 60px;
    }

    .batch-download-btn {
        padding: 5px 10px;
        background-color: #0284c7;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-size: 13px;
        transition: background-color 0.2s;
    }

    .batch-download-btn:hover {
        background-color: #0369a1;
    }

    .toggle-btn {
        background: none;        /* 无背景 */
        border: none;            /* 无边框 */
        font-size: 18px;         /* 字体大小18px */
        cursor: pointer;         /* 鼠标指针为手型 */
        color: #666;             /* 字体颜色 */
        width: 30px;             /* 宽度30px */
        height: 30px;            /* 高度30px */
        border-radius: 50%;      /* 圆形按钮 */
        display: flex;           /* flex布局 */
        align-items: center;     /* 垂直居中 */
        justify-content: center; /* 水平居中 */
        transition: background-color 0.2s; /* 背景色过渡 */
    }

    .toggle-btn:hover {
        background-color: #f5f5f5; /* 鼠标悬停时背景色 */
    }

    .tool-title {
        margin: 0;               /* 无外边距 */
        color: #333;             /* 字体颜色 */
        font-size: 16px;         /* 字体大小 */
        font-weight: bold;       /* 加粗 */
        flex-grow: 1;            /* 占满剩余空间 */
        text-align: center;      /* 文字居中 */
    }

    .tool-content {
        display: flex;           /* flex布局 */
        flex: 1;                 /* 占满剩余空间 */
        overflow: hidden;        /* 超出部分隐藏 */
    }

    .labels-panel {
        width: 120px;            /* 宽度120px */
        border-right: 1px solid #eee; /* 右侧边框 */
        overflow-y: auto;        /* 垂直方向可滚动 */
    }

    .label-item {
        padding: 10px 15px;      /* 内边距 */
        cursor: pointer;         /* 鼠标指针为手型 */
        color: #666;             /* 字体颜色 */
        font-size: 14px;         /* 字体大小 */
        transition: all 0.2s;    /* 所有属性过渡 */
    }

    .label-item:hover {
        background-color: #f5f5f5; /* 鼠标悬停背景色 */
    }

    .label-item.active {
        background-color: #e6f7ff; /* 选中状态背景色 */
        color: #1890ff;          /* 选中状态字体色 */
        border-left: 3px solid #1890ff; /* 左侧选中边框 */
    }

    .papers-panel {
        flex: 1;                 /* 占满剩余空间 */
        overflow-y: auto;        /* 垂直方向可滚动 */
    }

    .papers-header {
        padding: 10px 15px;      /* 内边距 */
        border-bottom: 1px solid #eee; /* 底部边框 */
        display: flex;           /* flex布局 */
        justify-content: space-between; /* 两端对齐 */
        align-items: center;     /* 垂直居中 */
    }

    .papers-count {
        color: #666;             /* 字体颜色 */
        font-size: 13px;         /* 字体大小 */
    }

    .paper-item {
        padding: 12px 15px;      /* 内边距 */
        border-bottom: 1px solid #f5f5f5; /* 底部边框 */
        cursor: pointer;         /* 鼠标指针为手型 */
        transition: background-color 0.2s; /* 背景色过渡 */
    }

    .paper-item:hover {
        background-color: #fafafa; /* 鼠标悬停背景色 */
    }

    .paper-title {
        margin: 0 0 5px 0;       /* 外边距 */
        font-size: 14px;         /* 字体大小 */
        color: #333;             /* 字体颜色 */
        white-space: nowrap;     /* 不换行 */
        overflow: hidden;        /* 超出部分隐藏 */
        text-overflow: ellipsis; /* 超出部分显示省略号 */
    }

    .paper-meta {
        display: flex;           /* flex布局 */
        justify-content: space-between; /* 两端对齐 */
        font-size: 12px;         /* 字体大小 */
        color: #999;             /* 字体颜色 */
    }

    .pagination {
        padding: 10px 15px;      /* 内边距 */
        display: flex;           /* flex布局 */
        justify-content: center; /* 水平居中 */
        gap: 5px;                /* 元素间距 */
        border-top: 1px solid #eee; /* 顶部边框 */
    }

    .page-btn {
        padding: 3px 10px;       /* 内边距 */
        border: 1px solid #ddd;  /* 边框 */
        border-radius: 4px;      /* 圆角 */
        background: white;       /* 背景色 */
        cursor: pointer;         /* 鼠标指针为手型 */
        font-size: 12px;         /* 字体大小 */
        transition: all 0.2s;    /* 所有属性过渡 */
    }

    .page-btn:disabled {
        opacity: 0.5;            /* 半透明 */
        cursor: not-allowed;     /* 禁止指针 */
    }

    .page-btn.active {
        background-color: #1890ff; /* 激活状态背景色 */
        color: white;            /* 激活状态字体色 */
        border-color: #1890ff;   /* 激活状态边框色 */
    }

    .collect-actions {
        padding: 10px 15px;      /* 内边距 */
        border-top: 1px solid #eee; /* 顶部边框 */
        display: flex;           /* flex布局 */
        gap: 8px;                /* 元素间距 */
    }

    .action-btn {
        flex: 1;                 /* 占满剩余空间 */
        padding: 6px 0;          /* 内边距 */
        border: none;            /* 无边框 */
        border-radius: 4px;      /* 圆角 */
        cursor: pointer;         /* 鼠标指针为手型 */
        font-size: 13px;         /* 字体大小 */
        transition: all 0.2s;    /* 所有属性过渡 */
    }

    .collect-btn {
        background-color: #4F46E5; /* 收藏按钮背景色 */
        color: white;            /* 字体颜色 */
    }

    .collect-btn:hover {
        background-color: #3A32B5; /* 鼠标悬停背景色 */
    }

    .batch-collect-btn {
        background-color: #10B981; /* 批量收藏按钮背景色 */
        color: white;            /* 字体颜色 */
    }

    .batch-collect-btn:hover {
        background-color: #059669; /* 鼠标悬停背景色 */
    }

    .solution-btn {
        background-color: #4A32B5; /* 清空按钮背景色 */
        color: white;            /* 字体颜色 */
    }

    .solution-btn:hover {
        background-color: #4f52B5; /* 清空按钮背景色 */
    }

    .export-error-btn {
        background-color: #e7bb0dff; /* 清空按钮背景色 */
        color: white;            /* 字体颜色 */
    }

    .export-error-btn:hover {
        background-color: #efbb0dff; /* 清空按钮背景色 */
    }

    .clear-btn {
        background-color: #ef4444; /* 清空按钮背景色 */
        color: white;            /* 字体颜色 */
    }

    .clear-btn:hover {
        background-color: #dc2626; /* 鼠标悬停背景色 */
    }

    .log-area {
        height: 180px;           /* 高度180px */
        border-top: 1px solid #eee; /* 顶部边框 */
        overflow-y: auto;        /* 垂直方向可滚动 */
        font-size: 12px;         /* 字体大小 */
    }

    .log-item {
        padding: 3px 15px;       /* 内边距 */
        border-bottom: 1px solid #f9f9f9; /* 底部边框 */
    }

    .log-success {
        color: #10B981;          /* 成功日志颜色 */
    }

    .log-error {
        color: #ef4444;          /* 错误日志颜色 */
    }

    .log-info {
        color: #3B82F6;          /* 信息日志颜色 */
    }

    .log-warning {
        color: #F59E0B;          /* 警告日志颜色 */
    }

    .loading {
        padding: 20px;           /* 内边距 */
        text-align: center;      /* 文字居中 */
        color: #666;             /* 字体颜色 */
        font-size: 13px;         /* 字体大小 */
    }

    .paper-actions {
        display: flex;           /* flex布局 */
        gap: 5px;                /* 元素间距 */
        margin-top: 8px;         /* 上外边距 */
    }

    .paper-action-btn {
        padding: 3px 8px;        /* 内边距 */
        font-size: 12px;         /* 字体大小 */
        border-radius: 3px;      /* 圆角 */
        border: none;            /* 无边框 */
        cursor: pointer;         /* 鼠标指针为手型 */
        transition: all 0.2s;    /* 所有属性过渡 */
    }
    .fb-view-btn {
        background-color: #e6f7ff;/* 查看按钮背景色 */
        color: #4c7bf4;             /* 字体颜色 */
    }

    .fb-view-btn:hover {
        background-color: #d1eaff; /* 鼠标悬停背景色 */
    }

    .view-btn {
        background-color: #f0f0f0; /* 查看按钮背景色 */
        color: #666;             /* 字体颜色 */
    }

    .view-btn:hover {
        background-color: #e0e0e0; /* 鼠标悬停背景色 */
    }

    .download-btn {
        background-color: #e6f7ff; /* 下载按钮背景色 */
        color: #0284c7;          /* 下载按钮字体颜色 */
    }

    .download-btn:hover {
        background-color: #d1eaff; /* 鼠标悬停背景色 */
    }

    .item-collect-btn {
        background-color: #e6f7ff; /* 收藏按钮背景色 */
        color: #1890ff;          /* 字体颜色 */
    }

    .item-collect-btn:hover {
        background-color: #d1eaff; /* 鼠标悬停背景色 */
    }

    .item-dis-collect-btn {
        background-color: #e6f7ff; /* 取消收藏按钮背景色 */
        color: #dd1432ff;          /* 字体颜色 */
    }

    .item-dis-collect-btn:hover {
        background-color: #d1eaff; /* 鼠标悬停背景色 */
    }

    .accuracy-filter {
        padding: 10px 15px;      /* 内边距 */
        border-bottom: 1px solid #eee; /* 底部边框 */
        display: flex;           /* flex布局 */
        align-items: center;     /* 垂直居中 */
        gap: 10px;               /* 元素间距 */
    }

    .accuracy-filter label {
        font-size: 12px;         /* 字体大小 */
        color: #666;             /* 字体颜色 */
    }

    .accuracy-filter input[type="range"] {
        flex: 1;                 /* 占满剩余空间 */
    }

    .accuracy-filter span {
        font-size: 12px;         /* 字体大小 */
        color: #666;             /* 字体颜色 */
        min-width: 50px;         /* 最小宽度50px */
    }

    /* 加载动画样式 */
    .spinner {
        width: 20px;             /* 宽度20px */
        height: 20px;            /* 高度20px */
        border: 2px solid rgba(0, 0, 0, 0.1); /* 边框 */
        border-radius: 50%;      /* 圆形 */
        border-top-color: #1890ff; /* 顶部边框颜色 */
        animation: spin 1s ease-in-out infinite; /* 旋转动画 */
        display: inline-block;   /* 行内块元素 */
        vertical-align: middle;  /* 垂直居中 */
        margin-right: 5px;       /* 右外边距 */
    }

    /* 旋转动画定义 */
    @keyframes spin {
        to { transform: rotate(360deg); }
    }

    /* 按钮加载状态 */
    .action-btn.loading {
        opacity: 0.7;            /* 半透明 */
        cursor: wait;            /* 等待指针 */
    }

    .action-btn.loading .spinner {
        display: inline-block;   /* 显示加载动画 */
    }

    /* 导出选项样式 */
    .export-options {
        margin-top: 15px;
        padding: 10px;
        background-color: #f9f9f9;
        border-radius: 4px;
    }

    .export-option-item {
        display: flex;
        align-items: center;
        margin-bottom: 8px;
        font-size: 14px;
    }

    .export-option-item input {
        margin-right: 8px;
    }

    .export-option-label {
        cursor: pointer;
    }

    .no-wrong-questions {
        color: #999;
        font-size: 13px;
        margin-top: 8px;
        padding-left: 24px;
        font-style: italic;
    }

    .no-unanswered-questions {
        color: #999;
        font-size: 13px;
        margin-top: 8px;
        padding-left: 24px;
        font-style: italic;
    }


    /* 题目类别选择弹窗样式 */
    .category-modal {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 10000;
        opacity: 0;
        visibility: hidden;
        transition: opacity 0.3s ease, visibility 0.3s ease;
    }

    .category-modal.show {
        opacity: 1;
        visibility: visible;
    }

    .category-modal-content {
        background-color: white;
        border-radius: 8px;
        width: 90%;
        max-width: 400px;
        box-shadow: 0 2px 20px rgba(0, 0, 0, 0.2);
        transform: translateY(-20px);
        transition: transform 0.3s ease;
    }

    .category-modal.show .category-modal-content {
        transform: translateY(0);
    }

    .category-modal-header {
        padding: 15px 20px;
        border-bottom: 1px solid #eee;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .category-modal-title {
        margin: 0;
        font-size: 16px;
        color: #333;
    }

    .category-modal-close {
        background: none;
        border: none;
        font-size: 20px;
        cursor: pointer;
        color: #999;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: background-color 0.2s;
    }

    .category-modal-close:hover {
        background-color: #f5f5f5;
        color: #333;
    }

    .category-modal-body {
        padding: 20px;
    }

    .category-item {
        display: flex;
        align-items: center;
        margin-bottom: 12px;
    }

    .category-item input {
        margin-right: 10px;
        width: 16px;
        height: 16px;
        cursor: pointer;
    }

    .category-item label {
        font-size: 14px;
        color: #333;
        cursor: pointer;
    }

    .category-modal-footer {
        padding: 10px 20px;
        border-top: 1px solid #eee;
        display: flex;
        justify-content: flex-end;
        gap: 10px;
    }

    .category-btn {
        padding: 6px 16px;
        border-radius: 4px;
        border: none;
        font-size: 14px;
        cursor: pointer;
        transition: background-color 0.2s;
    }

    .category-cancel {
        background-color: #f5f5f5;
        color: #666;
    }

    .category-cancel:hover {
        background-color: #e5e5e5;
    }

    .category-confirm {
        background-color: #4F46E5;
        color: white;
    }

    .category-confirm:hover {
        background-color: #3A32B5;
    }

    .category-select-all {
        margin-bottom: 15px;
        padding-bottom: 10px;
        border-bottom: 1px dashed #eee;
    }

    /* 批量下载进度条样式 */
    .batch-download-progress {
        margin-top: 10px;
        height: 6px;
        background-color: #f0f0f0;
        border-radius: 3px;
        overflow: hidden;
        display: none;
    }

    .batch-download-progress.active {
        display: block;
    }

    .progress-bar {
        height: 100%;
        background-color: #0284c7;
        width: 0%;
        transition: width 0.3s ease;
    }
`);

/**
 * 主应用类 - FenbiPaperTool
 * 封装了所有功能和状态管理
 */
class FenbiPaperTool {
    /**
     * 构造函数 - 初始化状态和绑定方法
     */
    constructor() {
        // 定义题目类别
        this.questionCategories = [
            { id: 'political', name: '政治理论' },
            { id: 'common-sense', name: '常识判断' },
            { id: 'verbal', name: '言语理解' },
            { id: 'quantity', name: '数量关系' },
            { id: 'logic', name: '判断推理' },
            { id: 'data', name: '资料分析' }
        ];

        // 状态管理 - 集中存储所有应用状态
        this.state = {
            currentLabelId: null,       // 当前选中的标签ID
            currentPage: 0,             // 当前页码
            totalPages: 1,              // 总页数
            pageSize: 10,               // 每页显示数量
            currentLabelType: 'xingce',// 标签类型目前兼容行测，职测
            allLabels: [],              // 所有标签列表
            allPapersByLabel: {},       // 按标签ID存储所有试卷
            currentPapers: [],          // 当前显示的试卷列表
            isHidden: true,             // 工具是否隐藏
            minAccuracy: 0,             // 最低正确率筛选值
            maxAccuracy: 100,           // 最高正确率筛选值
            isProcessing: false,        // 是否正在处理操作
            globalExerciseId: null,     // 全局存储的练习ID
            globalApiResponseData: null, // 全局存储的API响应数据
            globalWrongQuestionIds: null, //全局存储的错误问题ID列表
            globalUnAsweredQuestionIds: null, //全局存储的未答问题ID列表
            selectedCategories: [],     // 当前选中的类别
            currentPaper: null,         // 当前操作的试卷
            currentAction: null,        // 当前操作类型: 'collect' 或 'view'
            currentChapters: [],         // 当前试卷所有章节简介
            batchCollection: false,     // 是否正在进行批量收藏
            searchQuery: '',            // 搜索关键词
            batchDownloadPages: 1,      // 批量下载的页数
            isBatchDownloading: false,   // 是否正在批量下载
            currentStatus: 0,//当前练习的状态
            questionIds: [],//获取当前页面的问题ID
            questionIdsByType: [],//只用来存储收藏数据或者错题的问题ID，以防被污染
        };

        // 绑定方法的this上下文，确保在事件回调中this指向当前实例
        this.bindMethods();

        // 初始化应用
        this.init();
    }

    /**
     * 绑定方法的this上下文
     * 确保所有类方法在作为回调函数时，this仍然指向类实例
     */
    bindMethods() {
        this.createContainer = this.createContainer.bind(this);
        this.bindEvents = this.bindEvents.bind(this);
        this.fetchLabels = this.fetchLabels.bind(this);
        this.renderLabels = this.renderLabels.bind(this);
        this.fetchPapers = this.fetchPapers.bind(this);
        this.renderPapers = this.renderPapers.bind(this);
        this.collectPaperQuestions = this.collectPaperQuestions.bind(this);
        this.disCollectPaperQuestions = this.disCollectPaperQuestions.bind(this);
        this.batchCollectAllPapers = this.batchCollectAllPapers.bind(this);
        this.clearAllCollections = this.clearAllCollections.bind(this);
        this.getPaperSolution = this.getPaperSolution.bind(this);
        this.hookRequest = this.hookRequest.bind(this);
        this.pollForValue = this.pollForValue.bind(this);
        this.pushLog = this.pushLog.bind(this);
        this.showLoading = this.showLoading.bind(this);
        this.createCategoryModal = this.createCategoryModal.bind(this);
        this.showCategoryModal = this.showCategoryModal.bind(this);
        this.hideCategoryModal = this.hideCategoryModal.bind(this);
        this.handleCategorySelection = this.handleCategorySelection.bind(this);
        this.toggleSelectAllCategories = this.toggleSelectAllCategories.bind(this);
        this.performCollectionWithCategories = this.performCollectionWithCategories.bind(this);
        this.handleSearch = this.handleSearch.bind(this);
        this.resetSearch = this.resetSearch.bind(this);
        this.filterPapersBySearch = this.filterPapersBySearch.bind(this);
        this.downloadPaperPDF = this.downloadPaperPDF.bind(this);
        this.batchDownloadPapers = this.batchDownloadPapers.bind(this); // 批量下载方法绑定
        this.updateBatchDownloadProgress = this.updateBatchDownloadProgress.bind(this); // 进度更新方法绑定
    }

    /**
     * 初始化应用
     * 设置请求钩子，页面加载完成后初始化UI
     */
    init() {
        // 设置请求钩子，用于拦截特定请求获取数据
        this.hookRequest();

        // 页面加载完成后初始化UI
        window.addEventListener('load', () => {
            // 延迟1秒执行，确保页面完全加载
            setTimeout(() => {
                // 创建工具容器并添加到页面
                this.container = this.createContainer();
                document.body.appendChild(this.container);

                // 创建类别选择弹窗
                this.categoryModal = this.createCategoryModal();
                document.body.appendChild(this.categoryModal);

                // 加载试卷标签，并在完成后启动轮询检查
                this.pollForValue().then(() => {
                    console.log('✅ 试卷标签加载完成，开始启动检查');
                    // 标签加载完成后再启动轮询检查
                    this.fetchLabels();
                })
                    .catch((error) => {
                        console.error('❌ 试卷标签加载失败，仍尝试启动检查:', error);
                        // 即使标签加载失败，也尝试启动检查
                        this.pollForValue();
                    });
            }, 1000);
        });
    }

    /**
     * 创建工具的主界面容器
     * @returns {HTMLElement} 工具容器DOM元素
     */
    createContainer() {
        // 创建容器元素
        const container = document.createElement('div');
        // 设置初始样式类，默认隐藏
        container.className = 'paper-tool-container hidden';

        // 设置容器内部HTML结构，新增搜索框和批量下载区域
        container.innerHTML = `
            <div class="tool-header">
                <h3 class="tool-title">试卷浏览与收藏工具</h3>
                <button class="toggle-btn">+</button>
            </div>

    <!-- 考试类型下拉框 -->
    <div class="exam-type-container">
        <label for="exam-type" class="exam-type-label">考试类型:</label>
        <select id="exam-type" class="exam-type-dropdown">
            <option value="xingce" selected>行测</option>
            <option value="syzc">职测</option>
             <option value="ylzp">医疗招聘</option>
        </select>
    </div>

    <!-- 搜索区域 -->
    <div class="search-container">
        <input type="text" class="search-input" placeholder="输入试卷名称搜索...">
        <button class="search-btn">搜索</button>
        <button class="search-btn reset-btn">重置</button>
    </div>

    <!-- 批量下载区域 -->
    <div class="batch-download-container">
        <span class="batch-download-label">批量下载页数:</span>
        <input type="number" class="batch-download-pages" min="1" value="1">
        <button class="batch-download-btn">下载搜索结果</button>
        <div class="batch-download-progress">
            <div class="progress-bar"></div>
        </div>
    </div>

            <div class="tool-content">
                <div class="labels-panel"></div>
                <div class="papers-panel">
                    <div class="loading">加载标签中...</div>
                </div>
            </div>
            <div class="accuracy-filter">
                <label for="min-accuracy">最低正确率：</label>
                <input type="range" id="min-accuracy" min="0" max="100" value="${this.state.minAccuracy}">
                <span id="min-accuracy-value">${this.state.minAccuracy}%</span>
                <label for="max-accuracy">最高正确率：</label>
                <input type="range" id="max-accuracy" min="0" max="100" value="${this.state.maxAccuracy}">
                <span id="max-accuracy-value">${this.state.maxAccuracy}%</span>
            </div>
            <div class="collect-actions">
                <button class="action-btn batch-collect-btn">批量收藏</button>
                <button class="action-btn clear-btn">清空收藏</button>
                <button class="action-btn solution-btn">获取当前练习解析</button>
                <button class="action-btn export-error-btn">导出当前错题</button>
            </div>
            <div class="log-area"></div>
        `;

        // 为容器绑定事件处理函数
        this.bindEvents(container);

        return container;
    }

    /**
     * 创建题目类别选择弹窗
     * @returns {HTMLElement} 弹窗DOM元素
     */
    createCategoryModal() {
        const modal = document.createElement('div');
        modal.className = 'category-modal';

        // 构建弹窗HTML
        modal.innerHTML = `
            <div class="category-modal-content">
                <div class="category-modal-header">
                    <h3 class="category-modal-title">选择要收藏的题目类别</h3>
                    <button class="category-modal-close">&times;</button>
                </div>
                <div class="category-modal-body">
                    <div class="category-select-all">
                        <div class="category-item">
                            <input type="checkbox" id="select-all-categories" checked>
                            <label for="select-all-categories">全选</label>
                        </div>
                    </div>
                    ${this.questionCategories.map(category => `
                        <div class="category-item">
                            <input type="checkbox" id="category-${category.id}" checked>
                            <label for="category-${category.id}">${category.name}</label>
                        </div>
                    `).join('')}
                </div>
                <div class="category-modal-footer">
                    <button class="category-btn category-cancel">取消</button>
                    <button class="category-btn category-confirm">确认</button>
                </div>
            </div>
        `;

        // 绑定事件
        modal.querySelector('.category-modal-close').addEventListener('click', this.hideCategoryModal);
        modal.querySelector('.category-cancel').addEventListener('click', this.hideCategoryModal);
        modal.querySelector('.category-confirm').addEventListener('click', this.performCollectionWithCategories);
        modal.querySelector('#select-all-categories').addEventListener('change', this.toggleSelectAllCategories);

        // 绑定类别选择事件
        this.questionCategories.forEach(category => {
            modal.querySelector(`#category-${category.id}`).addEventListener('change', this.handleCategorySelection);
        });

        return modal;
    }

    /**
     * 显示类别选择弹窗
     * @param {Object} paper - 当前操作的试卷，批量收藏时可以为null
     * @param {string} action - 操作类型: 'collect' 或 'view'
     * @param {boolean} isBatch - 是否是批量收藏
     */
    showCategoryModal(paper, action = 'collect', isBatch = false) {

        // 保存当前操作的试卷和操作类型
        this.state.currentPaper = paper;
        this.state.currentAction = action;
        console.log(action);
        // 记录是否是批量收藏
        this.state.batchCollection = isBatch;
        if (action != 'clearCollect' && (this.state.currentLabelId === `all-${this.state.currentLabelType}` || this.state.currentLabelId === `all-exam-${this.state.currentLabelType}`)) {
            this.state.selectedCategories = [...this.questionCategories.map(c => c.id)];
            this.performCollectionWithCategories();
            return;
        }
        // 显示弹窗
        this.categoryModal.classList.add('show');

        // 重置为全选状态
        const checkboxes = this.categoryModal.querySelectorAll('.category-item input:not(#select-all-categories)');
        checkboxes.forEach(checkbox => {
            checkbox.checked = true;
        });
        this.categoryModal.querySelector('#select-all-categories').checked = true;

        // 记录当前选中的类别
        this.state.selectedCategories = [...this.questionCategories.map(c => c.id)];

        // 根据操作类型修改弹窗标题
        if (action === 'view') {
            this.categoryModal.querySelector('.category-modal-title').textContent =
                '选择要查看的题目类别';
        } else if (isBatch) {
            if (action === 'clearCollect') {
                this.categoryModal.querySelector('.category-modal-title').textContent =
                    '选择清空收藏的题目类别';
            } else {
                this.categoryModal.querySelector('.category-modal-title').textContent =
                    '选择批量收藏的题目类别';
            }
        } else {
            this.categoryModal.querySelector('.category-modal-title').textContent =
                '选择要收藏的题目类别';
        }
    }

    /**
     * 隐藏类别选择弹窗
     */
    hideCategoryModal() {
        this.categoryModal.classList.remove('show');
        //this.state.currentPaper = null; // 清除当前操作的试卷
    }

    /**
     * 处理类别选择变化
     */
    handleCategorySelection() {
        // 获取所有类别复选框
        const checkboxes = this.categoryModal.querySelectorAll('.category-item input:not(#select-all-categories)');
        const checkedCategories = [];

        // 收集选中的类别
        checkboxes.forEach(checkbox => {
            if (checkbox.checked) {
                const categoryId = checkbox.id.replace('category-', '');
                checkedCategories.push(categoryId);
            }
        });

        // 更新状态
        this.state.selectedCategories = checkedCategories;

        // 更新全选复选框状态
        const selectAllCheckbox = this.categoryModal.querySelector('#select-all-categories');
        selectAllCheckbox.checked = checkedCategories.length === this.questionCategories.length;
    }

    /**
     * 切换全选/取消全选
     */
    toggleSelectAllCategories() {
        const selectAllCheckbox = this.categoryModal.querySelector('#select-all-categories');
        const checkboxes = this.categoryModal.querySelectorAll('.category-item input:not(#select-all-categories)');

        // 全选或取消全选
        checkboxes.forEach(checkbox => {
            checkbox.checked = selectAllCheckbox.checked;
        });

        // 更新状态
        this.state.selectedCategories = selectAllCheckbox.checked
            ? [...this.questionCategories.map(c => c.id)]
            : [];
    }

    /**
     * 执行带类别的操作（收藏或查看解析）
     */
    async performCollectionWithCategories() {
        // 隐藏弹窗
        this.hideCategoryModal();

        // 记录选中的类别
        const selectedCategoryNames = this.state.selectedCategories
            .map(id => this.questionCategories.find(c => c.id === id)?.name || id)
            .join('、');

        let currentAction = '';
        switch (this.state.currentAction) {
            case 'view':
                currentAction = '查看';
                break;
            case 'clearCollect':
                currentAction = '清空收藏';
                break;
            default:
                currentAction = '收藏';
                break;
        }
        this.pushLog(`已选择${currentAction}类别：${selectedCategoryNames}`, 'info');

        // 根据操作类型执行不同操作
        if (this.state.currentAction === 'view' && this.state.currentPaper) {
            // 执行查看解析操作
            await this.getPaperSolution(this.state.currentPaper);
        } else if (this.state.batchCollection) {
            if (this.state.currentAction === 'clearCollect') {
                await this.clearAllCollections();
            } else {
                // 执行批量收藏
                await this.batchCollectAllPapers();
            }
        } else if (this.state.currentPaper) {
            // 执行单份试卷收藏
            await this.collectPaperQuestions(this.state.currentPaper);
        } else {
            this.pushLog('未找到试卷信息，操作失败', 'error');
        }
    }

    /**
     * 为容器绑定事件处理函数
     * @param {HTMLElement} container - 工具容器DOM元素
     */
    bindEvents(container) {
        // 获取DOM元素
        const minAccuracySlider = container.querySelector('#min-accuracy');
        const maxAccuracySlider = container.querySelector('#max-accuracy');
        const minAccuracyValue = container.querySelector('#min-accuracy-value');
        const maxAccuracyValue = container.querySelector('#max-accuracy-value');
        const toggleBtn = container.querySelector('.toggle-btn');
        const batchCollectBtn = container.querySelector('.batch-collect-btn');
        const clearBtn = container.querySelector('.clear-btn');
        const solutionBtn = container.querySelector('.solution-btn');
        const exportErrorBtn = container.querySelector('.export-error-btn');
        const searchInput = container.querySelector('.search-input');
        const searchBtn = container.querySelector('.search-btn:not(.reset-btn)');
        const resetBtn = container.querySelector('.reset-btn');
        const batchDownloadInput = container.querySelector('.batch-download-pages');
        const batchDownloadBtn = container.querySelector('.batch-download-btn');
        const examTypeDropdown = container.querySelector('#exam-type');

        // 绑定下拉框选择事件
        if (examTypeDropdown) {
            examTypeDropdown.addEventListener('change', (e) => {
                const selectedValue = e.target.value;
                const selectedText = e.target.options[e.target.selectedIndex].text;

                if (selectedValue) {
                    // 打印选中的值到控制台
                    console.log(`选中的考试类型: ${selectedText}, 对应值: ${selectedValue}`);
                    this.state.currentLabelType = selectedValue;
                    // 切换标签时重置搜索
                    this.state.searchQuery = '';
                    const searchInput = this.container.querySelector('.search-input');
                    if (searchInput) searchInput.value = '';
                    // 加载试卷标签
                    this.fetchLabels();
                }
            });
        }

        // 最低正确率滑块事件
        minAccuracySlider.addEventListener('input', () => {
            // 更新状态中的最低正确率值
            this.state.minAccuracy = parseInt(minAccuracySlider.value, 10);
            // 更新显示的数值
            minAccuracyValue.textContent = `${this.state.minAccuracy}%`;
            // 确保最低值不大于最高值
            if (this.state.minAccuracy > this.state.maxAccuracy) {
                this.state.minAccuracy = this.state.maxAccuracy;
                minAccuracySlider.value = this.state.maxAccuracy;
                minAccuracyValue.textContent = `${this.state.maxAccuracy}%`;
            }
        });

        // 最高正确率滑块事件
        maxAccuracySlider.addEventListener('input', () => {
            // 更新状态中的最高正确率值
            this.state.maxAccuracy = parseInt(maxAccuracySlider.value, 10);
            // 更新显示的数值
            maxAccuracyValue.textContent = `${this.state.maxAccuracy}%`;
            // 确保最高值不小于最低值
            if (this.state.maxAccuracy < this.state.minAccuracy) {
                this.state.maxAccuracy = this.state.minAccuracy;
                maxAccuracySlider.value = this.state.minAccuracy;
                maxAccuracyValue.textContent = `${this.state.minAccuracy}%`;
            }
        });

        // 批量收藏按钮点击事件
        batchCollectBtn.addEventListener('click', () => {
            // 如果正在处理操作，则不执行
            if (this.state.isProcessing) {
                this.pushLog('正在处理中，请稍后再试', 'warning');
                return;
            }
            // 显示类别选择弹窗，标记为批量收藏
            if (this.state.currentPapers.length > 0) {
                this.showCategoryModal(null, 'collect', true);
            } else {
                this.pushLog('没有可收藏的试卷', 'error');
            }

        });


        // 清空收藏按钮点击事件
        clearBtn.addEventListener('click', () => {
            // 如果正在处理操作，则不执行
            if (this.state.isProcessing) {
                this.pushLog('正在处理中，请稍后再试', 'warning');
                return;
            }
            // 执行清空收藏
            //this.clearAllCollections();
            // 显示类别选择弹窗，标记为批量收藏
            this.showCategoryModal(null, 'clearCollect', true);

        });

        // 获取解析按钮点击事件
        solutionBtn.addEventListener('click', () => {
            // 如果正在处理操作，则不执行
            if (this.state.isProcessing) {
                this.pushLog('正在处理中，请稍后再试', 'warning');
                return;
            }

            // 执行获取解析
            this.getSolutionByExerciseId();

        });

        // 获取导出错题按钮点击事件
        exportErrorBtn.addEventListener('click', () => {
            // 如果正在处理操作，则不执行
            if (this.state.isProcessing) {
                this.pushLog('正在处理中，请稍后再试', 'warning');
                return;
            }
            if (this.state.questionIdsByType != null && this.state.questionIdsByType.length > 0) {

                // 执行导出错题
                this.getSolutionsByType();

            } else {
                this.pushLog('没有获取到对应数据，请移步收藏或者错题详情页', 'warning');

            }
        });

        // 切换工具显示/隐藏状态
        toggleBtn.addEventListener('click', () => {
            // 切换状态
            this.state.isHidden = !this.state.isHidden;
            if (this.state.isHidden) {
                // 隐藏状态
                container.classList.add('hidden');
                toggleBtn.textContent = "+";
            } else {
                // 显示状态
                container.classList.remove('hidden');
                toggleBtn.textContent = "-";
            }
        });

        // 搜索相关事件绑定
        searchInput.addEventListener('keyup', (e) => {
            // 按Enter键触发搜索
            if (e.key === 'Enter') {
                this.handleSearch();
            }
        });

        searchBtn.addEventListener('click', this.handleSearch);
        resetBtn.addEventListener('click', this.resetSearch);

        // 批量下载相关事件
        batchDownloadInput.addEventListener('change', (e) => {
            let value = parseInt(e.target.value, 10) || 1;
            value = Math.max(1, value); // 确保最小值为1
            this.state.batchDownloadPages = value;
            e.target.value = value;
        });

        batchDownloadBtn.addEventListener('click', this.batchDownloadPapers);
    }

    /**
     * 更新批量下载进度条
     * @param {number} current - 当前下载数量
     * @param {number} total - 总下载数量
     */
    updateBatchDownloadProgress(current, total) {
        const progressContainer = this.container.querySelector('.batch-download-progress');
        const progressBar = this.container.querySelector('.progress-bar');

        if (current === 0) {
            progressContainer.classList.add('active');
            progressBar.style.width = '0%';
        } else {
            const percentage = Math.min(100, Math.round((current / total) * 100));
            progressBar.style.width = `${percentage}%`;

            // 下载完成后隐藏进度条
            if (current === total) {
                setTimeout(() => {
                    progressContainer.classList.remove('active');
                }, 1000);
            }
        }
    }

    /**
     * 处理搜索功能
     */
    handleSearch() {
        const searchInput = this.container.querySelector('.search-input');
        const query = searchInput.value.trim().toLowerCase();
        this.state.searchQuery = query;

        // 如果搜索词为空，直接重置
        if (!query) {
            this.resetSearch();
            return;
        }

        this.pushLog(`搜索试卷: "${query}"`, 'info');
        // 筛选试卷并重新渲染
        this.filterPapersBySearch();
    }

    /**
     * 重置搜索
     */
    resetSearch() {
        const searchInput = this.container.querySelector('.search-input');
        searchInput.value = '';
        this.state.searchQuery = '';
        this.pushLog('搜索已重置', 'info');
        // 重新获取当前标签的试卷列表
        this.updateCurrentPapers();
    }

    /**
     * 根据搜索词筛选试卷（支持顿号分隔的多关键词，要求全部匹配）
     */
    filterPapersBySearch() {
        if (!this.state.searchQuery || !this.state.currentLabelId) {
            // 如果没有搜索词或没有选中标签，显示所有试卷
            this.updateCurrentPapers();
            return;
        }

        // 获取当前标签的所有试卷
        const allPapers = this.state.allPapersByLabel[this.state.currentLabelId] || [];

        // 将搜索词按顿号分割成数组数组，并，并过滤空字符串
        const keywords = this.state.searchQuery
            .toLowerCase()
            .split('、')
            .map(keyword => keyword.trim())
            .filter(keyword => keyword);

        // 如果分割后没有有效关键词，显示所有试卷
        if (keywords.length === 0) {
            this.updateCurrentPapers();
            return;
        }

        // 进行多关键词模糊匹配，要求所有关键词都匹配
        const filteredPapers = allPapers.filter(paper => {
            const paperName = paper.name ?? paper.sheet.name;
            const paperNameLowerCase = paperName.toLowerCase();
            // 关键修改：将 some 改为 every
            return keywords.every(keyword => paperNameLowerCase.includes(keyword));
        });

        // 计算总页数
        this.state.totalPages = Math.ceil(filteredPapers.length / this.state.pageSize) || 1;
        // 确保当前页码有效
        if (this.state.currentPage >= this.state.totalPages) {
            this.state.currentPage = Math.max(0, this.state.totalPages - 1);
        }

        // 应用分页
        const startIndex = this.state.currentPage * this.state.pageSize;
        this.state.currentPapers = filteredPapers.slice(startIndex, startIndex + this.state.pageSize);

        this.pushLog(`找到 ${filteredPapers.length} 个同时匹配"${this.state.searchQuery}"所有关键词的试卷`, 'info');
        this.renderPapers();
    }

    /**
     * 更新当前显示的试卷列表（应用分页）
     */
    updateCurrentPapers() {
        if (!this.state.currentLabelId) return;

        // 获取当前标签的所有试卷
        const allPapers = this.state.allPapersByLabel[this.state.currentLabelId] || [];

        // 计算总页数
        this.state.totalPages = Math.ceil(allPapers.length / this.state.pageSize) || 1;
        // 确保当前页码有效
        if (this.state.currentPage >= this.state.totalPages) {
            this.state.currentPage = Math.max(0, this.state.totalPages - 1);
        }

        // 应用分页
        const startIndex = this.state.currentPage * this.state.pageSize;
        this.state.currentPapers = allPapers.slice(startIndex, startIndex + this.state.pageSize);

        this.renderPapers();
    }

    /**
     * 在试卷面板显示加载状态
     */
    showLoading() {
        const papersPanel = this.container.querySelector('.papers-panel');
        papersPanel.innerHTML = '<div class="loading">加载中...</div>';
    }

    /**
     * 向日志区域添加一条日志
     * @param {string} message - 日志消息
     * @param {string} type - 日志类型：info, success, error, warning
     */
    pushLog(message, type = 'info') {
        const logArea = this.container.querySelector('.log-area');
        // 创建日志项元素
        const logItem = document.createElement('div');
        logItem.className = `log-item log-${type}`;
        // 设置日志内容，包含时间戳
        logItem.innerHTML = `[${new Date().toLocaleTimeString()}] ${message}`;
        // 添加到日志区域
        logArea.appendChild(logItem);
        // 滚动到最新日志
        logArea.scrollTop = logArea.scrollHeight;
    }

    /**
     * HTTP请求封装
     * @param {Object} options - 请求选项
     * @returns {Promise} 返回Promise对象
     */
    httpRequest(options) {
        return new Promise((resolve, reject) => {
            // 使用GM_xmlhttpRequest发送请求，支持跨域
            GM_xmlhttpRequest({
                ...options,
                // 请求成功回调
                onload: (response) => {
                    if (response.status >= 200 && response.status < 300) {
                        // 成功状态，返回响应内容
                        resolve(response.responseText);
                    } else {
                        // 错误状态，返回错误信息
                        reject(new Error(`HTTP错误: ${response.status}`));
                    }
                },
                // 请求错误回调
                onerror: (error) => reject(error),
                // 请求中止回调
                onabort: () => reject(new Error('请求被中止')),
                // 超时时间15秒
                timeout: 15000
            });
        });
    }

    /**
    * 钩子请求，拦截特定请求获取exerciseId
    */
    hookRequest() {
        // 保存当前实例的引用
        const self = this;

        // 保存原始的open和send方法
        const originalOpen = XMLHttpRequest.prototype.open;
        const originalSend = XMLHttpRequest.prototype.send;

        // 重写open方法，保存请求URL
        XMLHttpRequest.prototype.open = function (method, url) {
            this._requestUrl = url;
            return originalOpen.apply(this, arguments);
        };

        // 重写send方法，添加事件监听
        XMLHttpRequest.prototype.send = function (body) {
            const url = this._requestUrl;
            const that = this;

            // 检查是否是目标请求combine/exercise/getExercise
            if (url && url.indexOf('/combine/exercise') !== -1) {
                console.log('🎯 拦截到目标请求 URL:', url);
                // 根据URL中的关键词动态设置考试类型
                if (url.indexOf('xingce') !== -1) {
                    self.state.currentLabelType = 'xingce';
                    console.log('📌 检测到行测类型请求，已设置当前类型为: xingce');
                } else if (url.indexOf('syzc') !== -1) {
                    self.state.currentLabelType = 'syzc';
                    console.log('📌 检测到职测类型请求，已设置当前类型为: syzc');
                } else if (url.indexOf('ylzp') !== -1) {
                    self.state.currentLabelType = 'ylzp';
                    console.log('📌 检测到医疗招聘类型请求，已设置当前类型为: ylzp');
                }

                // 监听请求状态变化，使用箭头函数保持this指向
                this.addEventListener('readystatechange', () => {
                    if (that.readyState === 4) { // 请求完成
                        if (that.status >= 200 && that.status < 300) { // 成功状态
                            try {
                                const responseText = that.responseText;
                                const data = JSON.parse(responseText);
                                // 提取exerciseId，使用self访问类实例
                                if (data && data.data && data.data.ancientExerciseId && data.data.ancientExerciseId.id) {
                                    self.state.globalExerciseId = data.data.ancientExerciseId.id;
                                    console.log('✅ 提取到的 exerciseId:', self.state.globalExerciseId);
                                } else {
                                    console.warn('⚠️ 返回数据结构不符合预期，未找到 exerciseId');
                                }
                            } catch (e) {
                                console.error('❌ 解析返回内容失败:', e);
                            }
                        } else {
                            console.error('❌ 请求失败，状态码:', that.status);
                        }
                    }
                });
            }

            // 检查是否是目标请求combine/exercise/
            if (url && url.indexOf('/combine/exercise/getSolution') !== -1) {
                console.log('🎯 拦截到目标请求 URL:', url);

                // 监听请求状态变化，使用箭头函数保持this指向
                this.addEventListener('readystatechange', () => {
                    if (that.readyState === 4) { // 请求完成
                        if (that.status >= 200 && that.status < 300) { // 成功状态
                            try {
                                const responseText = that.responseText;
                                const data = JSON.parse(responseText);
                                // 提取status=-1的id，使用self访问类实例
                                if (data && data.data && data.data.userAnswers) {
                                    // 假设 data 是你获取到的 userAnswers 对象
                                    const userAnswers = data.data.userAnswers;
                                    // 筛选出 status 为 -1 的项，并收集它们的 id
                                    const wrongIds = [];
                                    // 筛选出 status 为 10 的项，并收集它们的 id
                                    const unAnsweredIds = [];
                                    for (const key in userAnswers) {
                                        if (userAnswers.hasOwnProperty(key)) {
                                            const item = userAnswers[key];
                                            // 检查 status 是否为 -1
                                            if (item.status === -1) {
                                                wrongIds.push(item.id);
                                            }
                                            // 检查 status 是否为 -1
                                            if (item.status === 10) {
                                                unAnsweredIds.push(item.id);
                                            }
                                        }
                                    }
                                    self.state.globalWrongQuestionIds = wrongIds;
                                    self.state.globalUnAsweredQuestionIds = unAnsweredIds;
                                    console.log('✅ 提取到的错误题目ID:', self.state.globalWrongQuestionIds);
                                    console.log('✅ 提取到的未答题目ID:', self.state.globalUnAsweredQuestionIds);
                                } else {
                                    console.warn('⚠️ 返回数据结构不符合预期，未找到 userAnswers');
                                }
                            } catch (e) {
                                console.error('❌ 解析返回内容失败:', e);
                            }
                        } else {
                            console.error('❌ 请求失败，状态码:', that.status);
                        }
                    }
                });
            }

            // 检查是否是目标请求
            if (url && (url.indexOf(`api/xingce/questionIds`) !== -1 || url.indexOf(`api/syzc/questionIds`) !== -1 || url.indexOf(`api/ylzp/questionIds`) !== -1)) {
                console.log('🎯 拦截到目标请求 URL:', url);

                // 根据URL中的关键词动态设置考试类型
                if (url.indexOf('xingce') !== -1) {
                    self.state.currentLabelType = 'xingce';
                    console.log('📌 检测到行测类型请求，已设置当前类型为: xingce');
                } else if (url.indexOf('syzc') !== -1) {
                    self.state.currentLabelType = 'syzc';
                    console.log('📌 检测到职测类型请求，已设置当前类型为: syzc');
                } else if (url.indexOf('ylzp') !== -1) {
                    self.state.currentLabelType = 'ylzp';
                    console.log('📌 检测到医疗招聘类型请求，已设置当前类型为: ylzp');
                }

                // 监听请求状态变化，使用箭头函数保持this指向
                this.addEventListener('readystatechange', () => {
                    if (that.readyState === 4) { // 请求完成
                        if (that.status >= 200 && that.status < 300) { // 成功状态
                            try {
                                const responseText = that.responseText;
                                const data = JSON.parse(responseText);
                                self.state.questionIdsByType = data.results;

                            } catch (e) {
                                console.error('❌ 解析返回内容失败:', e);
                            }
                        } else {
                            console.error('❌ 请求失败，状态码:', that.status);
                        }
                    }
                });
            }

            // 调用原始的send方法
            return originalSend.apply(this, arguments);
        };
    }

    /**
     * 轮询检查特定页面并获取数据
     */
    async pollForValue() {

        // 定义所有需要匹配的前缀
        const TARGET_PATH_PREFIXES = ["/ti/exam/", "/spa/tiku/"];
        // 当前页面路径
        const currentPath = window.location.pathname;
        // 判断是否是目标页面（只要匹配任何一个前缀即可）
        const isTargetPage = TARGET_PATH_PREFIXES.some(prefix =>
            currentPath.startsWith(prefix)
        );

        if (!isTargetPage) {
            console.log(`❌ 当前页面路径（${currentPath}）不是目标页面（需以以下任一前缀开头：${TARGET_PATH_PREFIXES.join('、')}），跳过请求`);
            return;
        }

        // 根据URL中的关键词动态设置考试类型
        if (currentPath.indexOf('xingce') !== -1) {
            this.state.currentLabelType = 'xingce';
            console.log('📌 检测到行测类型请求，已设置当前类型为: xingce');
        } else if (currentPath.indexOf('syzc') !== -1) {
            this.state.currentLabelType = 'syzc';
            console.log('📌 检测到职测类型请求，已设置当前类型为: syzc');
        } else if (currentPath.indexOf('ylzp') !== -1) {
            this.state.currentLabelType = 'ylzp';
            console.log('📌 检测到医疗招聘类型请求，已设置当前类型为: ylzp');
        }

        if (currentPath.indexOf('/spa/tiku') == -1) {
            const exportErrorBtn = document.querySelector('.export-error-btn');
            exportErrorBtn.hidden = true;
        } else if (currentPath.indexOf('/ti/exam/') == -1) {
            const solutionBtn = document.querySelector('.solution-btn');
            solutionBtn.hidden = true;
        }

        // 如果已获取到WrongQuestionIds，则处理
        if (this.state.globalWrongQuestionIds !== null && this.state.globalWrongQuestionIds !== undefined) {
            console.log('✅ 目标页面+globalWrongQuestionIds 已存在', this.state.globalWrongQuestionIds);
        } else {
            console.log('❌ 目标页面，但 globalWrongQuestionIds 还不存在...');
        }

        // 如果已获取到exerciseId，则处理
        if (this.state.globalExerciseId !== null && this.state.globalExerciseId !== undefined) {
            console.log('✅ 目标页面+globalExerciseId 已存在', this.state.globalExerciseId);
            this.state.questionIds = await this.getExerciseQuestions(this.state.globalExerciseId);
        } else {
            console.log('❌ 目标页面，但 globalExerciseId 还不存在');
        }

        // 如果已获取到exerciseId，则处理
        if (this.state.questionIds !== null && this.state.questionIds !== undefined) {
            console.log('✅ 目标页面+questionIds 已存在', this.state.questionIds);

            const currentPath = window.location.pathname;

            if (this.state.globalExerciseId == null) {
                const exportErrorBtn = document.querySelector('.export-error-btn');
                exportErrorBtn.hidden = false;
            } else {
                const solutionBtn = document.querySelector('.solution-btn');

                if (currentPath.indexOf('/ti/exam/') !== -1) {
                    solutionBtn.hidden = false;
                }
            }
        } else {
            console.log('❌ 目标页面，但 globalExerciseId 还不存在');
        }

        // 更新下拉框选中状态以匹配当前类型
        const examTypeDropdown = document.querySelector('#exam-type');
        if (examTypeDropdown) {
            examTypeDropdown.value = this.state.currentLabelType;
        }

        // this.fetchLabels();
    }

    /**
     * 延迟函数
     * @param {number} ms - 延迟毫秒数
     * @returns {Promise} 返回Promise对象
     */
    sleep(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }

    /**
     * 渲染标签列表
     */
    renderLabels() {
        const labelsPanel = this.container.querySelector('.labels-panel');
        // 清空现有内容
        labelsPanel.innerHTML = '';

        // 遍历所有标签，创建标签项
        this.state.allLabels.forEach(label => {
            const labelItem = document.createElement('div');
            // 设置样式类，当前选中的标签添加active类
            labelItem.className = `label-item ${this.state.currentLabelId === label.id ? 'active' : ''}`;
            labelItem.textContent = label.name;
            // 绑定点击事件，切换标签
            labelItem.addEventListener('click', () => {
                // 切换标签时重置搜索
                this.state.searchQuery = '';
                const searchInput = this.container.querySelector('.search-input');
                if (searchInput) searchInput.value = '';

                this.state.currentLabelId = label.id;
                this.state.currentPage = 0; // 切换标签时重置到第一页
                this.fetchPapers(); // 获取该标签下的试卷
                this.renderLabels(); // 重新渲染标签列表，更新选中状态
            });
            labelsPanel.appendChild(labelItem);
        });
    }

    /**
     * 渲染试卷列表
     */
    renderPapers() {
        const papersPanel = this.container.querySelector('.papers-panel');
        // 清空现有内容
        papersPanel.innerHTML = '';

        // 创建试卷列表头部
        const header = document.createElement('div');
        header.className = 'papers-header';
        let length = this.state.allPapersByLabel[this.state.currentLabelId]?.length || 0;
        header.innerHTML = `<div class="papers-count">共 ${length} 份试卷</div>`;
        papersPanel.appendChild(header);

        // 创建试卷列表容器
        const papersList = document.createElement('div');
        papersList.className = 'papers-list';

        // 检查是否有试卷数据
        if (this.state.currentPapers.length === 0) {
            papersList.innerHTML = '<div class="loading">没有找到试卷</div>';
        } else {
            // 遍历试卷数据，创建试卷项
            this.state.currentPapers.forEach(paper => {
                const paperItem = document.createElement('div');
                paperItem.className = 'paper-item';
                const paperName = paper.name ?? paper.sheet.name;
                const isFinish = paper.key != undefined && paper.status == 1;

                // 设置试卷项内容，包含下载按钮
                paperItem.innerHTML = `
                    <h4 class="paper-title">${paperName}</h4>
                    <div class="paper-actions">
                        ${isFinish ? `<button class="paper-action-btn fb-view-btn" data-id="${paper.key}">粉笔解析</button>` : ''}
                        <button class="paper-action-btn item-view-btn" data-id="${paper.id}" data-name="${paperName}">查看解析</button>
                        <button class="paper-action-btn download-btn" data-id="${paper.id}" data-name="${paperName}">下载试卷</button>
                        <button class="paper-action-btn item-collect-btn" data-id="${paper.id}" data-name="${paperName}">收藏题目</button>
                        <button class="paper-action-btn item-dis-collect-btn" data-id="${paper.id}" data-name="${paperName}">取消收藏</button>
                    </div>
                `;

                // 跳转粉笔解析按钮事件
                const viewBtn = paperItem.querySelector('.fb-view-btn');
                if (viewBtn) { // 只有当按钮存在时才绑定事件
                    viewBtn.addEventListener('click', (e) => {
                        e.stopPropagation(); // 阻止事件冒泡

                        const paperId = e.currentTarget.getAttribute('data-id');
                        window.open(`https://spa.fenbi.com/ti/exam/solution/${paperId}?routecs=xingce`, "_blank");
                    });
                }

                // 查看解析按钮事件 - 点击时显示类别选择弹窗
                paperItem.querySelector('.item-view-btn').addEventListener('click', (e) => {
                    e.stopPropagation(); // 阻止事件冒泡
                    // 如果正在处理操作，则不执行
                    if (this.state.isProcessing) {
                        this.pushLog('正在处理中，请稍后再试', 'warning');
                        return;
                    }
                    const paperId = e.currentTarget.getAttribute('data-id');
                    const paperName = e.currentTarget.getAttribute('data-name');
                    // 显示类别选择弹窗，指定操作为查看解析
                    this.showCategoryModal({ id: paperId, name: paperName }, 'view');
                });

                // 下载试卷按钮事件
                paperItem.querySelector('.download-btn').addEventListener('click', (e) => {
                    e.stopPropagation(); // 阻止事件冒泡
                    // 如果正在处理操作，则不执行
                    if (this.state.isProcessing || this.state.isBatchDownloading) {
                        this.pushLog('正在处理中，请稍后再试', 'warning');
                        return;
                    }
                    const paperId = e.currentTarget.getAttribute('data-id');
                    const paperName = e.currentTarget.getAttribute('data-name');
                    this.downloadPaperPDF({ id: paperId, name: paperName });
                });

                // 收藏题目按钮事件 - 点击时显示类别选择弹窗
                paperItem.querySelector('.item-collect-btn').addEventListener('click', (e) => {
                    e.stopPropagation(); // 阻止事件冒泡

                    const paperId = e.currentTarget.getAttribute('data-id');
                    const paperName = e.currentTarget.getAttribute('data-name');
                    // 显示类别选择弹窗
                    this.showCategoryModal({ id: paperId, name: paperName }, 'collect');

                });

                // 取消收藏题目按钮事件
                paperItem.querySelector('.item-dis-collect-btn').addEventListener('click', (e) => {
                    e.stopPropagation(); // 阻止事件冒泡
                    // 如果正在处理操作，则不执行
                    if (this.state.isProcessing) {
                        this.pushLog('正在处理中，请稍后再试', 'warning');
                        return;
                    }
                    const paperId = e.currentTarget.getAttribute('data-id');
                    const paperName = e.currentTarget.getAttribute('data-name');
                    this.disCollectPaperQuestions({ id: paperId, name: paperName });
                });

                papersList.appendChild(paperItem);
            });
        }

        papersPanel.appendChild(papersList);

        // 创建分页控件
        const pagination = document.createElement('div');
        pagination.className = 'pagination';

        pagination.innerHTML = `
            <button class="page-btn prev-btn" ${this.state.currentPage === 0 ? 'disabled' : ''}>上一页</button>
            <button class="page-btn page-num active">${this.state.currentPage + 1}/${this.state.totalPages}</button>
            <button class="page-btn next-btn" ${this.state.currentPage >= this.state.totalPages - 1 ? 'disabled' : ''}>下一页</button>
        `;

        // 上一页按钮事件
        pagination.querySelector('.prev-btn').addEventListener('click', () => {
            if (this.state.currentPage > 0) {
                this.state.currentPage--;
                // 应用搜索和分页
                if (this.state.searchQuery) {
                    this.filterPapersBySearch();
                } else {
                    this.updateCurrentPapers();
                }
            }
        });

        // 下一页按钮事件
        pagination.querySelector('.next-btn').addEventListener('click', () => {
            if (this.state.currentPage < this.state.totalPages - 1) {
                this.state.currentPage++;
                // 应用搜索和分页
                if (this.state.searchQuery) {
                    this.filterPapersBySearch();
                } else {
                    this.updateCurrentPapers();
                }
            }
        });

        papersPanel.appendChild(pagination);
    }

    /**
     * 获取标签列表
     */
    async fetchLabels() {
        try {
            // 标签API地址
            const apiUrl = `https://tiku.fenbi.com/api/${this.state.currentLabelType}/subLabels?app=web&kav=100&av=100&hav=100&version=3.0.0.0`;

            // 发送请求
            const response = await this.httpRequest({
                method: 'GET',
                url: apiUrl,
                headers: {
                    'Accept': 'application/json, text/plain, */*',
                    'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                    'User-Agent': navigator.userAgent
                }
            });

            // 解析响应数据
            const data = JSON.parse(response);
            // 在标签列表前添加"所有练习"选项
            const allLabels = data || [];
            // 添加写死的"所有练习"标签作为第一个选项
            this.state.allLabels = [{
                id: `all-${this.state.currentLabelType}`,  // 可以使用特殊ID标识全部练习
                name: '所有练习'  // 写死的名称
            }, {
                id: `all-exam-${this.state.currentLabelType}`,  // 可以使用特殊ID标识全部试卷
                name: '所有试卷'  // 写死的名称
            }, ...allLabels];

            // 渲染标签列表
            this.renderLabels();

            // 默认选择国考标签
            if (this.state.allLabels.length > 0) {
                this.state.currentLabelId = this.state.allLabels[1].id;
                this.fetchPapers(); // 获取第一个标签下的试卷
                this.renderLabels(); // 重新渲染标签列表
            }
        } catch (error) {
            this.pushLog(`获取标签失败: ${error.message}`, 'error');
        }
    }

    /**
    * 获取标签下的所有试卷（包括所有分页）
    */
    async fetchAllPagesForLabel(labelId) {
        if (this.state.allPapersByLabel[labelId] && this.state.allPapersByLabel[labelId][0] == 'isProcessing') {
            return;
        }
        this.state.allPapersByLabel[labelId] = ['isProcessing'];

        let allItems = [];
        let currentPage = 0;
        let totalPages = 1;
        // 扩展判断条件，同时包含"all"和"all-exam"两种情况
        const isAllExercises = labelId === `all-${this.state.currentLabelType}` || labelId === `all-exam-${this.state.currentLabelType}`;
        // 提取公共请求配置（所有API请求共用的headers等）
        const requestConfig = {
            method: 'GET',
            headers: {
                'Accept': 'application/json, text/plain, */*',
                'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                'User-Agent': navigator.userAgent,
                'Cookie': document.cookie
            }
        };

        try {
            if (isAllExercises) {
                // 【练习数据分支】通过递归+游标获取所有练习
                const baseUrl = `https://tiku.fenbi.com/api/${this.state.currentLabelType}/category-exercises`;

                // 封装URL构建逻辑：根据游标cursor生成带参数的请求地址
                const buildUrl = (cursor) => {
                    const url = new URL(baseUrl);
                    url.searchParams.append('cursor', cursor); // 分页游标（用于加载下一页）
                    url.searchParams.append('count', 30);      // 每页条数
                    // 动态设置categoryId：all对应2，all-exam对应1
                    const categoryId = labelId === `all-${this.state.currentLabelType}` ? 2 : 1;
                    url.searchParams.append('categoryId', categoryId);
                    url.searchParams.append('noCacheTag', '409'); // 防缓存标记
                    url.searchParams.append('app', 'web');     // 应用标识
                    url.searchParams.append('kav', '100');     // 版本相关参数
                    url.searchParams.append('av', '100');
                    url.searchParams.append('hav', '100');
                    url.searchParams.append('version', '3.0.0.0');
                    return url.toString();
                };

                // 封装“请求单页练习数据”的逻辑：返回当前页数据 + 下一页游标
                const fetchExerciseData = async (cursor) => {
                    try {
                        const response = await this.httpRequest({
                            ...requestConfig,
                            url: buildUrl(cursor),
                        });
                        const data = JSON.parse(response);
                        return {
                            list: data.datas || [], // 当前页练习列表（兜底空数组避免报错）
                            nextCursor: data.cursor !== undefined ? data.cursor : -1, // 下一页游标（-1 表示无更多数据）
                        };
                    } catch (error) {
                        console.error(`请求 cursor=${cursor} 的练习数据失败:`, error);
                        throw error; // 向上层抛出错误，由调用方统一处理
                    }
                };

                // 递归获取所有练习数据（async 函数自动返回 Promise，确保异步完成后返回全量数据）
                const fetchAllData = async (currentCursor = 0, accumulatedData = []) => {
                    try {

                        // 1. 异步获取“当前页练习数据”
                        const { list, nextCursor } = await fetchExerciseData(currentCursor);
                        // 2. 累积数据（通过函数参数传递，避免依赖 React state 异步更新导致数据丢失）
                        const updatedData = [...accumulatedData, ...list];
                        // 3. 新增：记录“当前已获取的总数据量”
                        this.pushLog(`已获取 ${updatedData.length} 条练习数据`);
                        // 4. 终止条件：没有下一页时，返回最终全量数据
                        if (nextCursor === -1) {
                            console.log('所有练习数据获取完成，共', updatedData.length, '条');
                            this.handleAllDataComplete?.(updatedData); // 可选的“数据完成”回调（若需要）
                            return updatedData; // async 函数会自动将返回值包装为 Promise
                        }
                        // 5. 延迟 800ms 防止请求过于频繁，再递归获取下一页
                        await new Promise((resolve) => setTimeout(resolve, 500));
                        // 递归调用自身，并返回最终结果（递归完成后会自动冒泡到最外层 Promise）
                        return fetchAllData(nextCursor, updatedData);
                    } catch (error) {
                        // 错误处理：更新状态 + 向上层抛出“包含部分数据的错误”
                        const errorMsg = `获取练习数据失败: ${error.message || '未知错误'}`;
                        throw {
                            message: errorMsg,
                            partialData: accumulatedData, // 携带“已获取的部分数据”，方便调用方处理
                        };
                    }
                };

                // 等待递归完成，获取全量练习数据并返回
                allItems = await fetchAllData(0, []);

            } else {
                // 【试卷数据分支】通过“页码分页”获取所有试卷
                const baseUrl = `https://tiku.fenbi.com/api/${this.state.currentLabelType}/papers`;

                // 封装URL构建逻辑：根据页码page生成带参数的请求地址
                const buildUrl = (page) => {
                    const url = new URL(baseUrl);
                    url.searchParams.append('toPage', page);   // 目标页码
                    url.searchParams.append('pageSize', 100);  // 每页条数
                    url.searchParams.append('labelId', labelId); // 标签ID（筛选试卷）
                    url.searchParams.append('app', 'web');
                    url.searchParams.append('kav', '100');
                    url.searchParams.append('av', '100');
                    url.searchParams.append('hav', '100');
                    url.searchParams.append('version', '3.0.0.0');
                    return url.toString();
                };

                // 封装“请求单页试卷数据”的逻辑：返回当前页列表+总页数
                const fetchPageData = async (page) => {
                    const response = await this.httpRequest({
                        ...requestConfig,
                        url: buildUrl(page)
                    });
                    const data = JSON.parse(response);
                    return {
                        list: data.list || [], // 当前页试卷列表
                        totalPages: data.pageInfo?.totalPage || 1 // 总页数（默认1页）
                    };
                };

                // 1. 请求第一页试卷数据
                const firstPageResult = await fetchPageData(currentPage);
                allItems = allItems.concat(firstPageResult.list); // 拼接第一页数据
                totalPages = firstPageResult.totalPages;          // 获取总页数
                this.pushLog(`开始加载标签下的试卷，共 ${totalPages} 页`, 'info');

                // 2. 循环请求剩余页码的试卷（从第2页开始）
                for (currentPage = 1; currentPage < totalPages; currentPage++) {
                    this.pushLog(`加载第 ${currentPage + 1}/${totalPages} 页`);
                    const pageResult = await fetchPageData(currentPage);
                    allItems = allItems.concat(pageResult.list); // 拼接当前页数据
                    await this.sleep(500); // 延迟500ms，避免请求过于频繁
                }
            }

            // 公共成功逻辑：输出日志+返回全量数据
            this.pushLog(`成功加载 ${allItems.length} 条${isAllExercises ? '练习' : '试卷'}`, 'success');
            console.log('最终获取的所有数据:', allItems);
            return allItems;
        } catch (error) {
            // 错误处理：输出错误日志，返回已获取的部分数据
            this.pushLog(`获取${isAllExercises ? '练习' : '试卷'}失败: ${error.message}`, 'error');
            return allItems;
        }
    }


    /**
     * 获取当前标签的试卷列表（全量数据）
     */
    async fetchPapers() {
        // 如果没有选中的标签，直接返回
        if (!this.state.currentLabelId) return;

        // 检查是否已经加载过该标签的试卷
        if (this.state.allPapersByLabel[this.state.currentLabelId] && this.state.allPapersByLabel[this.state.currentLabelId][0] != 'isProcessing') {
            this.updateCurrentPapers();
            return;
        }

        // 显示加载状态
        this.showLoading();

        try {
            const labelId = this.state.currentLabelId

            // 获取该标签下的所有试卷（所有分页）
            const allPapers = await this.fetchAllPagesForLabel(labelId);

            if (allPapers) {
                // 存储全量数据
                this.state.allPapersByLabel[labelId] = allPapers;
            }

            if (this.state.allPapersByLabel[labelId][0] != 'isProcessing' && labelId == this.state.currentLabelId) {
                // 更新当前显示的试卷（应用分页）
                this.updateCurrentPapers();
            }


        } catch (error) {
            const papersPanel = this.container.querySelector('.papers-panel');
            papersPanel.innerHTML = `<div class="loading">加载失败: ${error.message}</div>`;
            this.pushLog(`获取试卷失败: ${error.message}`, 'error');
            console.error(error);
        }
    }

    async delPapers(allPapers) {
        // 提取 id 并确保为数字类型
        const idArray = allPapers.map(item => Number(item.id));
        console.log('id数组:', idArray);

        const batchSize = 30;
        const totalBatches = Math.ceil(idArray.length / batchSize);
        let successCount = 0;
        const failedBatches = [];

        for (let i = 0; i < totalBatches; i++) {
            const start = i * batchSize;
            const end = start + batchSize;
            const batchData = idArray.slice(start, end);
            const batchIndex = i + 1;
            console.log(`第${batchIndex}批数据:`, batchData);

            try {
                await this.httpRequest({
                    url: `https://tiku.fenbi.com/api/xingce/exercises/del?app=web&kav=100&av=121&hav=100&version=3.0.0.0`,
                    method: 'POST',
                    headers: {
                        'Accept': 'application/json, text/plain, */*',
                        'Accept-Encoding': 'gzip, deflate, br, zstd', // 可选，但加上更匹配
                        'Accept-Language': 'zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6', // 可选
                        'Content-Type': 'application/json',
                        'Cookie': document.cookie,
                        'Origin': 'https://www.fenbi.com',
                        'Priority': 'u=1, i',
                        'Referer': 'https://www.fenbi.com/',
                        'User-Agent': navigator.userAgent,
                        // 可选：添加 Sec-Ch-Ua（浏览器标识，截图中存在）
                        'Sec-Ch-Ua': '"Chromium";v="130", "Microsoft Edge";v="130", "Not?A_Brand";v="99"'
                    },
                    data: JSON.stringify(batchData) // 纯数组格式，与截图一致
                });

                successCount++;
                console.log(`第 ${batchIndex}/${totalBatches} 批发送成功`);
            } catch (error) {
                failedBatches.push({
                    index: batchIndex,
                    data: batchData,
                    error: error.message || '未知错误'
                });
                console.error(`第 ${batchIndex}/${totalBatches} 批发送失败:`, error);
            }
        }

        console.log(`\n批量处理完成：总批次${totalBatches}，成功${successCount}，失败${failedBatches.length}`);
    }

    /**
     * 下载试卷PDF
     * @param {Object} paper - 试卷对象
     * @param {boolean} isBatch - 是否是批量下载中的一个
     * @returns {boolean} 是否下载成功
     */
    async downloadPaperPDF(paper, isBatch = false) {

        const paperName = paper.name ?? paper.sheet.name;
        let exerciseId = paper.id;
        if (!isBatch) {
            this.pushLog(`开始下载试卷：《${paperName}》`, 'info');
        }
        if (this.state.currentLabelId != `all-${this.state.currentLabelType}` && this.state.currentLabelId != `all-exam-${this.state.currentLabelType}`) {

            // 步骤1：检查并创建练习
            const exerciseCreated = await this.createExercise(paper);
            if (!exerciseCreated || !paper.exercise?.id) {
                this.pushLog('❌ 无法下载，未获取到练习ID', 'error');
                return false;
            }
            exerciseId = paper.exercise.id;
        }


        // 步骤2：构建下载URL并触发下载
        const downloadUrl = `https://tiku.fenbi.com/api/${this.state.currentLabelType}/exercises/${exerciseId}/pdf`;

        try {
            // 先检查URL是否有效
            await this.httpRequest({
                method: 'HEAD',
                url: downloadUrl,
                headers: {
                    'Cookie': document.cookie,
                    'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                    'User-Agent': navigator.userAgent
                }
            });

            // 创建隐藏的a标签来触发下载
            const a = document.createElement('a');
            a.href = downloadUrl;
            // 清理文件名中的特殊字符
            const fileName = `${paperName.replace(/[\/:*?"<>|]/g, '-')}.pdf`;
            a.download = fileName;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);

            if (!isBatch) {
                this.pushLog(`✅ 已开始下载《${paperName}》`, 'success');
            }
            return true;
        } catch (error) {
            if (!isBatch) {
                this.pushLog(`❌ 下载失败：${error.message}`, 'error');
            }
            console.error('下载试卷出错:', error);
            return false;
        }
    }

    /**
     * 批量下载搜索结果中的试卷
     */
    async batchDownloadPapers() {
        // 检查是否正在处理或批量下载中
        if (this.state.isProcessing || this.state.isBatchDownloading) {
            this.pushLog('正在处理中，请稍后再试', 'warning');
            return;
        }

        // 检查是否有搜索结果
        if (this.state.currentPapers.length === 0) {
            this.pushLog('没有可下载的试卷，请先搜索或选择标签', 'error');
            return;
        }

        // 获取要下载的页数
        const pagesToDownload = this.state.batchDownloadPages;
        const totalPages = this.state.totalPages;
        const actualPages = Math.min(pagesToDownload, totalPages);

        // 计算要下载的试卷总数
        let totalPapers = 0;
        const papersToDownload = [];

        // 收集所有要下载的试卷
        for (let page = 0; page < actualPages; page++) {
            const startIndex = page * this.state.pageSize;
            let endIndex = startIndex + this.state.pageSize;
            // 获取当前标签的所有试卷，并应用多关键词全匹配筛选
            const allPapers = this.state.searchQuery
                ? (() => {
                    // 将搜索词按顿号分割成数组，并过滤空字符串
                    const keywords = this.state.searchQuery
                        .toLowerCase()
                        .split('、')
                        .map(keyword => keyword.trim())
                        .filter(keyword => keyword);

                    // 如果没有有效关键词，返回所有试卷
                    if (keywords.length === 0) {
                        return this.state.allPapersByLabel[this.state.currentLabelId] || [];
                    }

                    // 应用多关键词全匹配筛选
                    return this.state.allPapersByLabel[this.state.currentLabelId]?.filter(paper => {
                        const paperName = paper.name.toLowerCase();
                        return keywords.every(keyword => paperName.includes(keyword));
                    }) || [];
                })()
                : this.state.allPapersByLabel[this.state.currentLabelId] || [];

            // 确保不超出范围
            endIndex = Math.min(endIndex, allPapers.length);


            // 添加到下载列表
            papersToDownload.push(...allPapers.slice(startIndex, endIndex));
        }

        totalPapers = papersToDownload.length;

        if (totalPapers === 0) {
            this.pushLog('没有找到符合条件的试卷', 'error');
            return;
        }

        this.state.isBatchDownloading = true;
        this.pushLog(`开始批量下载 ${totalPapers} 份试卷（共 ${actualPages} 页）`, 'info');
        this.updateBatchDownloadProgress(0, totalPapers);

        let successCount = 0;
        let failCount = 0;

        try {
            // 逐个下载试卷
            for (let i = 0; i < totalPapers; i++) {
                // 显示当前进度
                this.pushLog(`正在下载 ${i + 1}/${totalPapers}：${papersToDownload[i].name ?? papersToDownload[i].sheet.name}`, 'info');

                // 下载试卷
                const success = await this.downloadPaperPDF(papersToDownload[i], true);

                // 更新计数
                if (success) {
                    successCount++;
                } else {
                    failCount++;
                    this.pushLog(`❌ 下载失败：${papersToDownload[i].name ?? papersToDownload[i].sheet.name}`, 'error');
                }

                // 更新进度条
                this.updateBatchDownloadProgress(i + 1, totalPapers);

                // 每下载2个试卷后暂停一下，避免请求过于频繁
                if ((i + 1) % 2 === 0) {
                    await this.sleep(2000);
                } else {
                    await this.sleep(1000);
                }
            }

            this.pushLog(`批量下载完成！成功：${successCount} 份，失败：${failCount} 份`, 'success');
        } catch (error) {
            this.pushLog(`批量下载过程出错：${error.message}`, 'error');
        } finally {
            this.state.isBatchDownloading = false;
        }
    }

    /**
     * 创建练习
     * @param {Object} paper - 试卷对象
     * @returns {boolean} 是否创建成功
     */
    async createExercise(paper) {
        const paperId = paper.id;
        const name = paper.name || '未知试卷';

        // 获取当前标签的所有试卷
        const allPapers = this.state.allPapersByLabel[`all-exam-${this.state.currentLabelType}`] || [];

        // 查找匹配paperId的试卷（根据截图中结构，试卷对象的paperId字段存储在sheet.paperId中）
        const matchedPaper = allPapers.find(item => item.sheet?.paperId === paperId);

        // 如果找到匹配项则打印
        if (matchedPaper) {
            console.log('找到匹配的试卷:', matchedPaper);
            paper = matchedPaper;
            return true;
        }
        this.pushLog(`🆕 正在创建试卷 "${name}"的相关练习 ...`);
        // 每处理完一份试卷休息1min，避免请求过于频繁
        await this.sleep(60000);
        // 练习创建表单数据
        const form = {
            type: 1,
            paperId: paperId,
            exerciseTimeMode: 2
        };

        try {
            // 转换表单数据为URLSearchParams格式
            const formData = new URLSearchParams();
            Object.entries(form).forEach(([k, v]) => formData.append(k, v));
            // 发送创建练习请求
            const createExerciseResponse = await this.httpRequest({
                url: `https://tiku.fenbi.com/api/${this.state.currentLabelType}/exercises?app=web&kav=100&av=100&hav=100&version=3.0.0.0`,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded',
                    'Cookie': document.cookie,
                    'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                    'User-Agent': navigator.userAgent
                },
                data: formData.toString()
            });

            // 检查响应是否为空
            if (!createExerciseResponse) {
                this.pushLog(`❌ 创建练习失败，试卷：${name}，响应为空`, 'error');
                return false;
            }

            // 解析响应数据
            let exerciseResponse = JSON.parse(createExerciseResponse);
            let exerciseId = exerciseResponse.id;
            if (exerciseId) {
                // 保存练习ID到试卷对象
                paper.exercise = { id: exerciseId };
                this.pushLog(`✅ 练习创建成功，ID: ${exerciseId}`, 'success');
                return true;
            } else {
                this.pushLog(`❌ 创建练习失败，试卷：${name}`, 'error');
                return false;
            }

        } catch (err) {
            this.pushLog(`❌ 创建练习出错：${err.message}`, 'error');
            return false;
        }
    }

    /**
     * 获取练习中的题目
     * @param {string} exerciseId - 练习ID
     * @returns {Array} 题目ID列表
     */
    async getExerciseQuestions(exerciseId) {
        try {
            // 发送请求获取练习详情
            const response = await this.httpRequest({
                url: `https://tiku.fenbi.com/api/${this.state.currentLabelType}/exercises/${exerciseId}`,
                method: 'GET',
                headers: {
                    'Cookie': document.cookie,
                    'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                    'User-Agent': navigator.userAgent
                }
            });

            // 解析响应数据，提取题目ID列表
            const data = JSON.parse(response);
            this.state.currentStatus = data?.status || 0;
            this.state.currentChapters = data?.sheet?.chapters || [];

            return data?.sheet?.questionIds || [];
        } catch (error) {
            this.pushLog(`❌ 获取题目失败：${error.message}`, 'error');
            console.error(error);
            return [];
        }
    }

    /**
     * 获取已收藏的题目ID
     * @param {Array} questionIds - 题目ID列表
     * @returns {Array} 已收藏的题目ID列表
     */
    async getCollectedQuestionIds(questionIds) {
        try {
            // 构建请求URL
            let url = `https://tiku.fenbi.com/api/${this.state.currentLabelType}/collects`;
            if (questionIds.length > 0) {
                url += `?ids=${questionIds.join(',')}`;
            }

            // 发送请求
            const response = await this.httpRequest({
                url,
                method: 'GET',
                headers: {
                    'Cookie': document.cookie,
                    'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                    'User-Agent': navigator.userAgent
                }
            });

            // 解析响应数据
            const data = JSON.parse(response);
            const collectedIds = Array.isArray(data) ? data : [];
            this.pushLog(`🔍 已收藏 ${collectedIds.length} 道题目`, 'info');
            return collectedIds;
        } catch (error) {
            this.pushLog(`❌ 查询收藏状态失败：${error.message}`, 'error');
            return [];
        }
    }

    /**
     * 获取题目元数据（包括准确率）
     * @param {Array} questionIds - 题目ID列表
     * @returns {string} 响应数据字符串
     */
    async getQuestionMetaByIds(questionIds) {
        try {
            // 发送请求获取题目元数据
            let questions = await this.httpRequest({
                url: `https://tiku.fenbi.com/api/${this.state.currentLabelType}/question/meta?ids=${questionIds.join(',')}`,
                method: "GET",
                headers: {
                    'Cookie': document.cookie,
                    'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                    'User-Agent': navigator.userAgent
                }
            });

            return questions;
        } catch (error) {
            this.pushLog(`❌ 获取题目准确率失败：${error.message}`, 'error');
            return null;
        }
    }

    /**
     * 根据选中的类别筛选题目
     * @param {Array} questionIds - 题目ID列表
     * @returns {Array} 筛选后的题目ID列表（无匹配时返回空数组表示跳过）
     */
    async filterQuestionsByCategories(questionIds) {
        // 检查是否全选了所有类别
        const isSelectAll = this.state.selectedCategories.length === this.questionCategories.length;
        if (isSelectAll) {
            this.pushLog('已选择全部类别，不进行章节筛选', 'info');
            return questionIds; // 全选时直接返回所有题目
        }

        // 验证章节数据是否存在
        if (!this.state.currentChapters || !Array.isArray(this.state.currentChapters)) {
            this.pushLog('未获取到章节信息，无法按类别筛选，将跳过该试卷', 'warning');
            return []; // 无章节信息时返回空数组表示跳过
        }

        // 筛选出需要处理的类别
        const targetCategories = this.state.selectedCategories;
        if (targetCategories.length === 0) {
            this.pushLog('没有选择任何类别，返回全部题目', 'info');
            return questionIds;
        }

        // 定义类别关键词映射表，用于匹配章节名称
        const categoryKeywords = {
            'political': ['政治', '时政', '政策'],
            'common-sense': ['常识', '基础知识', '公共基础'],
            'verbal': ['言语', '语言', '理解'],
            'quantity': ['数量', '数字', '计算'],
            'logic': ['逻辑', '推理', '科学'],
            'data': ['资料', '数据', '分析']
        };

        // 收集符合条件的题目ID
        let result = [];
        let currentPosition = 0; // 记录在总题目列表中的当前位置

        // 遍历所有章节，查找与选中类别匹配的章节
        this.state.currentChapters.forEach(chapter => {

            // 跳过没有题目数量信息的章节
            let questionCount = chapter.questionCount ?? chapter.questionIds.length ?? 0;

            if (questionCount <= 0) {
                return;
            }

            this.pushLog(`分析章节: ${chapter.name}, 题目数量: ${questionCount}`, 'info');

            // 检查当前章节是否匹配任何选中的类别
            const matchedCategory = targetCategories.find(category => {
                // 检查章节名称是否包含该类别的任何关键词
                return categoryKeywords[category]?.some(keyword =>
                    chapter.name.includes(keyword)
                );
            });

            // 如果找到匹配的类别，提取该章节的题目
            if (matchedCategory) {
                const categoryName = this.questionCategories.find(c => c.id === matchedCategory)?.name;
                this.pushLog(`找到匹配章节: ${chapter.name} -> 类别: ${categoryName}`, 'success');

                // 计算该章节在总题目列表中的起始和结束索引
                const startIndex = currentPosition;
                const endIndex = Math.min(currentPosition + questionCount, questionIds.length);

                // 提取对应范围的题目ID
                const categoryQuestions = questionIds.slice(startIndex, endIndex);
                result = [...result, ...categoryQuestions];

                this.pushLog(`从章节提取 ${categoryQuestions.length} 道${categoryName}题目`, 'success');
            }

            // 更新当前位置指针
            currentPosition += questionCount;
        });

        if (result.length === 0) {
            this.pushLog('没有找到与所选类别匹配的章节，将跳过该试卷', 'warning');
            return []; // 没有匹配题目时返回空数组表示跳过
        }

        return result;
    }

    /**
     * 收藏未收藏的题目
     * @param {Array} unCollectedIds - 未收藏的题目ID列表
     * @returns {number} 成功收藏的数量
     */
    async collectUnCollectedQuestions(unCollectedIds) {
        let successCount = 0;
        // 遍历未收藏的题目ID
        for (let j = 0; j < unCollectedIds.length; j++) {
            const qid = unCollectedIds[j];
            try {
                // 发送收藏请求
                await this.httpRequest({
                    url: `https://tiku.fenbi.com/api/${this.state.currentLabelType}/collects/${qid}`,
                    method: 'POST',
                    headers: {
                        'Cookie': document.cookie,
                        'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                        'User-Agent': navigator.userAgent
                    }
                });
                successCount++;
                this.pushLog(`✅ 收藏成功：第 ${j + 1}/${unCollectedIds.length} 题 (ID: ${qid})`, 'success');
            } catch (err) {
                this.pushLog(`❌ 收藏失败：第 ${j + 1} 题 (${qid})`, 'error');
                await this.sleep(500); // 延迟500ms后重试
                // 重试一次
                try {
                    await this.httpRequest({
                        url: `https://tiku.fenbi.com/api/${this.state.currentLabelType}/collects/${qid}`,
                        method: 'POST',
                        headers: {
                            'Cookie': document.cookie,
                            'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                            'User-Agent': navigator.userAgent
                        }
                    });
                    successCount++;
                    this.pushLog(`✅ 重试成功：第 ${j + 1} 题 (${qid})`, 'success');
                    console.error(err);
                } catch (retryErr) {
                    this.pushLog(`🔁 重试失败：第 ${j + 1} 题 (${qid})`, 'error');
                    console.error(retryErr);
                }
            }
            // 避免请求过于频繁，每个请求间隔300ms
            await this.sleep(300);
        }
        return successCount;
    }

    /**
     * 收藏试卷中的题目
     * @param {Object} paper - 试卷对象
     */
    async collectPaperQuestions(paper) {
        // 设置处理状态为true，防止重复操作
        this.state.isProcessing = true;
        try {
            const paperName = paper.name ?? paper.sheet.name;
            let exerciseId = paper.id;
            this.pushLog(`开始处理试卷：《${paperName}》`, 'info');
            if (this.state.currentLabelId != `all-${this.state.currentLabelType}` && this.state.currentLabelId != `all-exam-${this.state.currentLabelType}`) {

                // 步骤1：检查并创建练习
                const exerciseCreated = await this.createExercise(paper);
                if (!exerciseCreated || !paper.exercise?.id) {
                    this.pushLog('❌ 无法继续，未获取到练习ID', 'error');
                    return;
                }
                exerciseId = paper.exercise.id;
            }

            // 步骤2：获取题目
            const questionIds = await this.getExerciseQuestions(exerciseId);
            if (questionIds.length === 0) {
                this.pushLog('ℹ️ 没有找到题目', 'info');
                return;
            }

            // 步骤3：根据选中的类别筛选题目
            const categoryFilteredIds = await this.filterQuestionsByCategories(questionIds);
            if (categoryFilteredIds.length === 0) {
                this.pushLog('ℹ️ 没有找到符合所选类别的题目', 'info');
                return;
            }

            // 步骤4-1：获取题目元数据并按准确率筛选
            const metaIds = await this.getQuestionMetaByIds(categoryFilteredIds);
            const parsedMetaIds = JSON.parse(metaIds);
            const accuracyFilteredIds = parsedMetaIds
                .filter(q => q.correctRatio >= this.state.minAccuracy && q.correctRatio <= this.state.maxAccuracy)
                .map(q => q.id);
            this.pushLog(`✅ 获取到 ${accuracyFilteredIds.length} 道符合准确率范围的题目`, 'success');

            // 步骤4-2：获取已收藏题目
            const collectedIds = await this.getCollectedQuestionIds(accuracyFilteredIds);

            // 步骤5：收藏未收藏的题目
            const unCollectedIds = accuracyFilteredIds.filter(qid => !collectedIds.includes(qid));
            if (unCollectedIds.length === 0) {
                this.pushLog('✅ 所有题目均已收藏', 'success');
                return;
            }

            this.pushLog(`需要收藏 ${unCollectedIds.length} 道题目`, 'info');
            const successCount = await this.collectUnCollectedQuestions(unCollectedIds);
            this.pushLog(`🎉 收藏完成，成功 ${successCount}/${unCollectedIds.length} 道`, 'success');
        } finally {
            // 无论成功失败，都重置处理状态
            this.state.isProcessing = false;
        }
    }

    /**
     *
     * @param {Array} collectedIds - 已经收藏的题目ID列表
     */
    async disCollectByCollectedIds(collectedIds) {

        this.pushLog(`🗑️ 开始删除 ${collectedIds.length} 道已收藏题目`, 'info');

        let deleteCount = 0;
        // 遍历删除每个收藏的题目
        for (const qid of collectedIds) {
            try {
                await this.httpRequest({
                    url: `https://tiku.fenbi.com/api/${this.state.currentLabelType}/collects/${qid}`,
                    method: 'DELETE',
                    headers: {
                        'Cookie': document.cookie,
                        'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                        'User-Agent': navigator.userAgent
                    }
                });
                deleteCount++;
                this.pushLog(`✅ 已删除：${qid} (${deleteCount}/${collectedIds.length})`, 'success');
            } catch (err) {
                this.pushLog(`❌ 删除失败：${qid}`, 'error');
            }
            // 每个删除请求间隔200ms
            await this.sleep(200);
        }

        this.pushLog(`🎉 清理完成，共删除 ${deleteCount} 道收藏题目`, 'success');
        return deleteCount;
    }

    /**
     * 取消收藏试卷中的题目
     * @param {Object} paper - 试卷对象
     */
    async disCollectPaperQuestions(paper) {

        // 设置处理状态为true，防止重复操作
        this.state.isProcessing = true;
        try {
            const paperName = paper.name ?? paper.sheet.name;
            let exerciseId = paper.id;
            this.pushLog(`开始处理试卷：《${paperName}》`, 'info');
            if (this.state.currentLabelId != `all-${this.state.currentLabelType}` && this.state.currentLabelId != `all-exam-${this.state.currentLabelType}`) {

                // 步骤1：检查并创建练习
                const exerciseCreated = await this.createExercise(paper);
                if (!exerciseCreated || !paper.exercise?.id) {
                    this.pushLog('❌ 无法继续，未获取到练习ID', 'error');
                    return;
                }
                exerciseId = paper.exercise.id;
            }
            // 步骤2：获取题目
            const questionIds = await this.getExerciseQuestions(exerciseId);
            if (questionIds.length === 0) {
                this.pushLog('ℹ️ 没有找到题目', 'info');
                return;
            }

            // 步骤4：获取已收藏题目
            const collectedIds = await this.getCollectedQuestionIds(questionIds);

            // 步骤5：取消收藏这些题目
            await this.disCollectByCollectedIds(collectedIds);

        } finally {
            // 无论成功失败，都重置处理状态
            this.state.isProcessing = false;
        }
    }

    /**
    * 获取评论前置数据相关
    * @returns {Object} 数据
    */
    async getEpisodesByIds(questionIds) {

        try {
            // 发送请求获取剧集数据
            let result = await this.httpRequest({
                url: `https://ke.fenbi.com/api/gwy/v3/episodes/tiku_episodes_with_multi_type?tiku_ids=${questionIds.join(',')}&tiku_prefix=xingce&tiku_type=5`,
                method: "GET",
                headers: {
                    'Cookie': document.cookie,
                    'Referer': 'https://ke.fenbi.com/gwy/',
                    'User-Agent': navigator.userAgent
                }
            });
            return JSON.parse(result).data;
        } catch (error) {
            console.log(`❌ 获取评论前置数据失败：${error.message}`, 'error');
            return {};
        }
    }

    /**
     * 批量收藏当前标签下的所有试卷（完整最终版：无冲突+视频下载修复+精准截取文件名（去公务员））
     */
    async batchCollectAllPapers() {

        // 获取当前标签的所有试卷
        const allPapers = this.state.currentPapers || [];
        console.log(allPapers);

        // 检查是否有试卷数据
        if (allPapers.length === 0) {
            this.pushLog('❌ 没有可收藏的试卷', 'error');
            return;
        }

        // 如果是批量收藏且没有选择类别，使用默认类别
        if (this.state.batchCollection && this.state.selectedCategories.length === 0) {
            this.state.selectedCategories = [...this.questionCategories.map(c => c.id)];
        }

        // 设置处理状态为true
        this.state.isProcessing = true;
        const batchBtn = this.container.querySelector('.batch-collect-btn');
        const originalText = batchBtn.textContent;
        batchBtn.innerHTML = '<span class="spinner"></span>处理中';
        batchBtn.disabled = true;


        // ==============================================
        // 核心业务逻辑
        // ==============================================
        try {
            let totalSuccess = 0; // 总成功收藏数量
            let totalFailed = 0;  // 总失败试卷数量

            this.pushLog(`开始批量收藏 ${allPapers.length} 份试卷`, 'info');

            // 遍历所有试卷
            for (let i = 0; i < allPapers.length; i++) {
                const paper = allPapers[i];
                const paperName = paper.name ?? paper.sheet.name;
                this.pushLog(`\n处理第 ${i + 1}/${allPapers.length} 份：《${paperName}》`, 'info');

                try {
                    let exerciseId = paper.id;

                    // 检查并创建练习（原有逻辑）
                    if (this.state.currentLabelId != `all-${this.state.currentLabelType}` && this.state.currentLabelId != `all-exam-${this.state.currentLabelType}`) {
                        const exerciseCreated = await this.createExercise(paper);
                        if (!exerciseCreated || !paper.exercise?.id) {
                            this.pushLog('❌ 跳过此试卷', 'error');
                            totalFailed++;
                            continue;
                        }
                        exerciseId = paper.exercise.id;
                    }

                    console.log(exerciseId);
                    // 获取题目（原有逻辑）
                    const questionIds = await this.getExerciseQuestions(exerciseId);
                    if (questionIds.length === 0) {
                        this.pushLog('ℹ️ 没有找到题目，跳过', 'warning');
                        continue;
                    }
                    console.log(questionIds);

                    // 按类别筛选题目（原有逻辑）
                    const categoryFilteredIds = await this.filterQuestionsByCategories(questionIds);
                    if (categoryFilteredIds.length === 0) {
                        this.pushLog('ℹ️ 没有找到符合所选类别的题目，跳过', 'info');
                        continue;
                    }
                    console.log(categoryFilteredIds);

                    // 按准确率筛选题目（原有逻辑）
                    const metaIds = await this.getQuestionMetaByIds(categoryFilteredIds);
                    const parsedMetaIds = JSON.parse(metaIds);

                    const filteredIds = parsedMetaIds
                        .filter(q => q.correctRatio >= this.state.minAccuracy && q.correctRatio <= this.state.maxAccuracy)
                        .map(q => q.id);
                    if (filteredIds.length === 0) {
                        this.pushLog('ℹ️ 没有符合准确率条件的题目，跳过', 'info');
                        continue;
                    }
                    console.log(filteredIds);

                    // 步骤4-2：获取已收藏题目
                    const collectedIds = await this.getCollectedQuestionIds(filteredIds);

                    // 步骤5：收藏未收藏的题目
                    const unCollectedIds = filteredIds.filter(qid => !collectedIds.includes(qid));
                    if (unCollectedIds.length === 0) {
                        this.pushLog('✅ 所有题目均已收藏', 'success');
                        continue;
                    }
                    console.log(unCollectedIds);
                    // 执行收藏（原有逻辑）
                    const successCount = await this.collectUnCollectedQuestions(unCollectedIds);
                    totalSuccess += successCount;
                    this.pushLog(`✅ 完成收藏，成功 ${successCount}/${unCollectedIds.length} 道`, 'success');

                } catch (error) {
                    this.pushLog(`❌ 处理试卷时出错：${error.message}`, 'error');
                    console.error(error);
                    totalFailed++;
                }
            }

            // 最终结果汇总
            this.pushLog(`\n🎉 批量收藏完成，共成功收藏 ${totalSuccess} 道题目，${totalFailed} 份试卷处理失败`, 'success');

        } finally {
            // 重置处理状态和按钮
            this.state.isProcessing = false;
            this.state.batchCollection = false; // 重置批量收藏状态
            batchBtn.innerHTML = originalText;
            batchBtn.disabled = false;
        }
    }

    /**
    * 清空所有已收藏的题目
    * 功能说明：通过用户确认后，获取所有收藏题目ID，按类别筛选后批量取消收藏，
    * 过程中显示加载状态，完成后反馈操作结果
    */
    async clearAllCollections() {
        /** 用户确认环节 - 防止误操作 */
        const userConfirmed = confirm('确定要清空所有已收藏的题目吗？此操作不可恢复！');
        if (!userConfirmed) {
            this.pushLog('ℹ️ 用户取消了清空收藏操作', 'info');
            return;
        }

        /** 初始化加载状态 - 提升用户体验 */
        this.state.isProcessing = true;
        const clearBtn = this.container.querySelector('.clear-btn');

        /** 保存按钮原始状态，便于后续恢复 */
        const originalText = clearBtn.textContent;
        const originalDisabled = clearBtn.disabled;

        /** 更新按钮为加载状态 */
        clearBtn.innerHTML = '<span class="spinner"></span>清理中';
        clearBtn.disabled = true;

        let deleteSuccessCount = 0;

        try {
            /** 获取所有收藏的题目ID */
            const requestUrl = `https://tiku.fenbi.com/api/${this.state.currentLabelType}/collects/keypoint-tree?timeRange=0&order=desc&app=web&kav=100&av=100&hav=100&version=3.0.0.0`;

            this.pushLog('🔍 开始获取收藏题目列表...', 'info');
            const response = await this.httpRequest({
                url: requestUrl,
                method: 'GET',
                headers: {
                    'Cookie': document.cookie,
                    'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                    'User-Agent': navigator.userAgent
                }
            });

            /** 解析响应数据 - 增加数据校验 */
            if (!response) {
                throw new Error('未获取到有效响应数据');
            }

            let collectedData = [];
            try {
                collectedData = JSON.parse(response);
            } catch (parseError) {
                throw new Error(`数据解析失败：${parseError.message}`);
            }

            /** 存储当前章节数据并提取所有收藏题目ID */
            this.state.currentChapters = collectedData || [];
            const allCollectedIds = [];
            collectedData.forEach(chapter => {
                if (Array.isArray(chapter.questionIds)) {
                    allCollectedIds.push(...chapter.questionIds);
                }
            });

            /** 校验是否有可删除的收藏 */
            if (allCollectedIds.length === 0) {
                this.pushLog('ℹ️ 没有找到任何已收藏的题目', 'info');
                return;
            }
            this.pushLog(`📋 共检测到 ${allCollectedIds.length} 道已收藏题目`, 'info');

            /** 按类别筛选题目 - 仅保留符合当前类别的题目ID */
            const filteredIds = await this.filterQuestionsByCategories(allCollectedIds);
            if (filteredIds.length === 0) {
                this.pushLog('ℹ️ 没有找到符合所选类别的收藏题目', 'info');
                return;
            }
            this.pushLog(`🔍 筛选后符合条件的题目共 ${filteredIds.length} 道`, 'info');

            /** 执行取消收藏操作 */
            deleteSuccessCount = await this.disCollectByCollectedIds(filteredIds);
            this.pushLog(`✅ 成功清空 ${deleteSuccessCount} 道收藏题目`, 'success');

        } catch (error) {
            /** 错误处理 - 详细记录错误信息 */
            this.pushLog(`❌ 清空收藏失败：${error.message}`, 'error');
            console.error('清空收藏操作出错：', error);

        } finally {
            /** 恢复状态 - 无论成功失败都要重置按钮状态 */
            this.state.isProcessing = false;
            clearBtn.innerHTML = originalText;
            clearBtn.disabled = originalDisabled;
            this.pushLog('📌 清空收藏操作已结束', 'info');
        }
    }

    // 分批请求解决方案数据（每次最多200条）
    async getSolutionsInBatches(questionIds) {
        const BATCH_SIZE = 200; // 每批最大数量
        const allSolutions = [];
        const totalBatches = Math.ceil(questionIds.length / BATCH_SIZE);

        // 循环处理每一批
        for (let i = 0; i < totalBatches; i++) {
            // 计算当前批次的起始和结束索引
            const startIndex = i * BATCH_SIZE;
            const endIndex = startIndex + BATCH_SIZE;
            const batchIds = questionIds.slice(startIndex, endIndex);

            try {
                // 调用原接口获取当前批次数据
                const batchData = await this.getSolutionsByQuestionIds(batchIds);
                const data = JSON.parse(batchData);

                if (data[0] != null) {
                    allSolutions.push(...data);
                }
                // 可选：添加延迟避免请求过于频繁
                if (i < totalBatches - 1) {
                    await new Promise(resolve => setTimeout(resolve, 100));
                }
            } catch (error) {
                console.error(`第 ${i + 1} 批请求失败:`, error);
                // 可根据需求决定是否继续或抛出错误
                // throw new Error(`获取解决方案失败，批次 ${i+1} 出错`);
            }
        }

        return allSolutions;
    }

    /**
    * 根据不同类型返回解析 类型包括：收藏、错题 暂未作区分
    * @returns
    */
    async getSolutionsByType() {
        this.state.isProcessing = true;
        try {
            const questionIds = this.state.questionIdsByType;
            const solutions = await this.getSolutionsInBatches(questionIds);

            if (solutions.length === 0) {
                alert("没有获取到数据,请检查是否在详情页、检查当前网页显示类型与脚本考试类型是否对应");
                return;
            }

            const metaIds = await this.getQuestionMetaByIds(questionIds);
            const parsedMetaIds = JSON.parse(metaIds);
            const data = this.processingData(solutions, parsedMetaIds);

            this.pushLog(`✅ 成功获取 ${data.length} 道题目`, 'success');
            const name = `下载 ${data.length} 道题目`;
            this.showSolutionWindow(data, name, true);
        } catch (error) {
            // 可以在这里处理错误，比如打印日志
            console.error("获取解析失败:", error);
        } finally {
            this.state.isProcessing = false;
        }
    }

    /**
     * 获取题目解析
     * @param {Array} questionIds - 题目ID列表
     * @returns {string} 响应数据字符串
     */
    async getSolutionsByQuestionIds(questionIds) {
        try {
            // 发送请求获取题目解析
            let solutions = await this.httpRequest({
                url: `https://tiku.fenbi.com/api/${this.state.currentLabelType}/solutions?ids=${questionIds.join(',')}`,
                method: "GET",
                headers: {
                    'Cookie': document.cookie,
                    'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                    'User-Agent': navigator.userAgent
                }
            });

            return solutions;
        } catch (error) {
            this.pushLog(`❌ 获取题目解析失败：${error.message}`, 'error');
            return null;
        }
    }

    /**
     * 根据练习获取解析
     * @param {Integer} exerciseId
     * @param {string} name
     * @returns
     */
    async getSolutionByExerciseId(exerciseId, name) {

        if (!exerciseId && !this.state.globalExerciseId) {
            this.pushLog('❌ 无法继续，未获取到练习ID', 'error');
            return;
        }

        this.state.isProcessing = true;

        if (!exerciseId) {
            exerciseId = this.state.globalExerciseId;
        }
        // 步骤1：获取题号
        const questionIds = await this.getExerciseQuestions(exerciseId);
        if (questionIds.length === 0) {
            this.pushLog('ℹ️ 没有找到题目', 'info');
            return;
        }

        // 步骤2：根据选中的类别筛选题目（如果有选择）
        const categoryFilteredIds = await this.filterQuestionsByCategories(questionIds);
        if (categoryFilteredIds.length === 0) {
            this.pushLog('ℹ️ 没有找到符合所选类别的题目', 'info');
            return;
        }

        this.state.globalExerciseId = exerciseId;
        this.state.questionIds = categoryFilteredIds;

        const qids = this.state.questionIds;

        // 并行获取episode信息
        this.state.episodeMap = await this.getEpisodesByIds(qids);

        // 创建获取解析的Promise
        const solutionPromise = this.getSolutionsByQuestionIds(categoryFilteredIds)
            .then(response => JSON.parse(response));

        // 创建获取meta信息的Promise
        const metaPromise = this.getQuestionMetaByIds(categoryFilteredIds)
            .then(response => JSON.parse(response));

        // 并行执行所有异步操作
        const [questionResponse, parsedMetaIds] = await Promise.all([
            solutionPromise,
            metaPromise
        ]);

        // 等待 pollForValue 完成后再处理后续逻辑
        this.pollForValue().then(async () => {

            // 在 pollForValue 完成后执行数据处理
            const filteredData = this.processingData(questionResponse, parsedMetaIds);

            // 如果已经完成的还需要收集错题
            if (this.state.currentStatus == 1) {
                const reportResponse = await this.getReportByExerciseId(exerciseId);
                if (reportResponse != null) {
                    const report = JSON.parse(reportResponse);

                    const answers = report.answers;
                    // 筛选出所有 status 为 -1 的项
                    this.state.globalWrongQuestionIds = answers.filter(item => item.status === -1)
                        .map(item => item.questionId);
                    // 筛选出所有 status 为 10 的项
                    this.state.globalUnAsweredQuestionIds = answers.filter(item => item.status === 10)
                        .map(item => item.questionId);
                }
            }
            this.pushLog(`✅ 成功获取 ${filteredData.length} 道题目的解析`, 'success');

            if (!name) {
                name = "当前解析";
            }

            // 调用显示解析窗口的方法，传入处理好的解析数据和试卷名称
            this.showSolutionWindow(filteredData, name, true);
        }).finally(() => {
            // 设置处理状态为false
            this.state.isProcessing = false;
        });
    }

    /**
     * 处理数据
     * @param {*} data
     * @param {*} parsedMetaIds
     * @returns
     */
    processingData(data, parsedMetaIds) {

        // 将数组转换为以id为key的对象（使用Object.fromEntries更简洁）
        const result = Object.fromEntries(parsedMetaIds.map(item => [item.id, item]));

        // 处理解析数据
        return Object.entries(data).map(([key, value]) => {
            const { id, type, content, accessories, solution, material, source, correctAnswer } = value;

            return {
                key: id,
                type,
                content,
                options: accessories?.[0]?.options,
                correctRatio: result[id]?.correctRatio,
                mostWrongAnswer: result[id]?.mostWrongAnswer,
                correctAnswer,
                solution,
                source,
                // 条件添加material属性
                ...(material != null && { material })
            };
        });
    }

    /**
     * 获取练习报告
     * @param {Integer} exerciseId
     * @returns
     */
    async getReportByExerciseId(exerciseId) {
        try {
            // 发送请求获取题目解析
            const response = await this.httpRequest({
                url: `https://tiku.fenbi.com/api/${this.state.currentLabelType}/exercises/${exerciseId}/report/v2`,
                method: "GET",
                headers: {
                    'Cookie': document.cookie,
                    'Referer': `https://tiku.fenbi.com/${this.state.currentLabelType}/`,
                    'User-Agent': navigator.userAgent
                }
            });

            return response;

        } catch (error) {
            this.pushLog(`❌ 获取练习报告失败：${error.message}`, 'error');
        }
    }

    /**
     * 获取试卷解析并在新窗口展示
     * @param {Object} paper - 试卷对象
     */
    async getPaperSolution(paper) {

        try {
            const paperName = paper.name ?? paper.sheet.name;
            let exerciseId = paper.id;
            this.pushLog(`开始获取试卷解析：《${paperName}》`, 'info');
            if (this.state.currentLabelId != `all-${this.state.currentLabelType}` && this.state.currentLabelId != `all-exam-${this.state.currentLabelType}`) {

                // 步骤1：检查并创建练习
                const exerciseCreated = await this.createExercise(paper);
                if (!exerciseCreated || !paper.exercise?.id) {
                    this.pushLog('❌ 无法继续，未获取到练习ID', 'error');
                    return;
                }
                exerciseId = paper.exercise.id;
            }
            await this.getSolutionByExerciseId(exerciseId, paperName);

        } catch (error) {
            this.pushLog(`❌ 获取解析失败：${error.message}`, 'error');
        }
    }

    /**
        * 创建并并显示解析窗口，支持按材料分组导出，相同材料材料只显示一次
        * 只有当存在材料时，解析才单独成页
        * @param {Array} solutions - 解析数据数组（所有题目）
        * @param {string} paperName - 试卷名称
        * @param {Boolean} includeSolution - 是否包含解析
        * @returns 
        */
    showSolutionWindow(solutions, paperName, includeSolution) {
        // 1. 验证数据有效性
        if (!solutions || !Array.isArray(solutions) || solutions.length === 0) {
            this.pushLog('❌ 解析数据为空或格式错误', 'error');
            return;
        }

        // 2. 按材料分组 - 相同材料的题目放在一组
        const groupedByMaterial = [];
        const materialMap = new Map();

        solutions.forEach(solution => {
            // 使用材料内容作为键，如果没有材料则使用特殊标识
            const materialKey = solution.material?.id ? solution.material?.id : `__no_material_${Date.now()}_${Math.random()}`;

            if (!materialMap.has(materialKey)) {
                // 创建新的材料组
                const newGroup = {
                    materialKey: materialKey,
                    material: solution.material?.content || null,
                    hasMaterial: !!solution.material?.content, // 标记是否有材料
                    questions: []
                };
                groupedByMaterial.push(newGroup);
                materialMap.set(materialKey, newGroup);
            }

            // 将题目添加到对应的材料组
            materialMap.get(materialKey).questions.push(solution);
        });

        // 3. 创建新弹窗
        const solutionWindow = window.open('', '_blank', 'width=827,height=1169,scrollbars=yes');
        if (!solutionWindow) {
            this.pushLog('❌ 弹窗被浏览器拦截，请请允许弹出窗口后重试', 'error');
            return;
        }

        // 4. 设置弹窗标题
        if (includeSolution) {
            solutionWindow.document.title = `${paperName} - 题目解析`;
        } else {
            solutionWindow.document.title = `${paperName}`;
        }

        // 存储导出相关状态 - 包含分页逻辑
        const exportStore = {
            isExporting: false,
            currentPage: 0,
            totalPages: 0, // 后面会计算
            exportOptions: {
                includeMaterial: true,
                includeOptions: true,
                includeSolution: includeSolution,
                quality: 0.95,
                pageOrientation: 'portrait',
                exportType: 'all'
            }
        };

        // 5. 构建基础DOM结构
        const buildBasicDOM = () => {
            const doc = solutionWindow.document;
            doc.open();

            // 创建文档声明
            const doctype = doc.implementation.createDocumentType('html', '', '');
            doc.appendChild(doctype);

            // 创建html元素
            const html = doc.createElement('html');
            html.lang = 'zh-CN';
            doc.appendChild(html);

            // 创建head元素
            const head = doc.createElement('head');
            html.appendChild(head);

            // 添加meta标签
            const metaCharset = doc.createElement('meta');
            metaCharset.charset = 'UTF-8';
            head.appendChild(metaCharset);

            const metaViewport = doc.createElement('meta');
            metaViewport.name = 'viewport';
            metaViewport.content = 'width=device-width, initial-scale=1.0';
            head.appendChild(metaViewport);

            // 添加标题
            const title = doc.createElement('title');
            if (includeSolution) {
                title.textContent = `${paperName} - 题目解析`;
            } else {
                title.textContent = `${paperName}`;
            }
            head.appendChild(title);

            // 添加样式
            const style = doc.createElement('style');
            style.textContent = `
body { font-family: "Microsoft YaHei", "SimSun", sans-serif; line-height: 1.6; padding: 20px; background-color: #f9f9f9; }
.container { max-width: 794px; margin: 0 auto; background: white; padding: 30px; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); }
.header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; border-bottom: 2px solid #4F46E5; padding-bottom: 10px; }
.loading { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); display: flex; justify-content: center; align-items: center; color: white; font-size: 18px; z-index: 1000; }
.spinner { border: 5px solid rgba(255,255,255,0.3); border-radius: 50%; border-top: 5px solid white; width: 50px; height: 50px; animation: spin 1s linear infinite; margin-right: 15px; }
@keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
.export-btn { background-color: #4F46E5; color: white; border: none; padding: 8px 16px; border-radius: 4px; cursor: pointer; display: flex; align-items: center; gap: 8px; }
.export-btn:disabled { background-color: #888; cursor: not-allowed; }
.question { margin-bottom: 30px; padding-bottom: 20px; border-bottom: 1px solid #eee; }
.question-number { font-weight: bold; font-size: 18px; margin-bottom: 10px; color: #333; }
.material, .content, .solution, .options, .correct-ratio, .source, .choice, .correct { margin-bottom: 15px; }
.material-title, .content-title, .solution-title, .options-title, .correct-ratio-title, .source-title, .choice-title, .correct-title { font-weight: bold; color: #4F46E5; margin-bottom: 5px; }
.correct, .correct-ratio, .source, .choice { display: flex; align-items: center; gap: 8px; line-height: 1; }
.correct-title, .correct-text, .correct-ratio-title, .correct-ratio-text, .choice-title, .choice-text, .source-title, .source-text { vertical-align: middle; margin: 0; padding: 0;  font-size: 16px; }
.progress-container { position: absolute; bottom: 30px; left: 0; width: 100%; padding: 0 20px; box-sizing: border-box; }
.progress-bar { height: 8px; background-color: rgba(255,255,255,0.3); border-radius: 4px; overflow: hidden; }
.progress-fill { height: 100%; background-color: white; width: 0%; transition: width 0.3s ease; }
.export-preview { padding: 0 !important; border-radius: 0 !important; box-shadow: none !important; }
.resource-progress { margin-top: 10px; font-size: 14px; }
/* 导出选项样式 */
.export-options { margin-top: 15px; padding: 10px; background-color: #f9f9f9; border-radius: 4px; }
.export-option-item { display: flex; align-items: center; margin-bottom: 8px; font-size: 14px; }
.export-option-item input { margin-right: 8px; }
.export-option-label { cursor: pointer; }
.no-wrong-questions { color: #999; font-size: 13px; margin-top: 8px; padding-left: 24px; font-style: italic; }
.no-unanswered-questions { color: #999; font-size: 13px; margin-top: 8px; padding-left: 24px; font-style: italic; }
/* 用于导出时隐藏不需要的部分 */
.hide-section { display: none !important; }
.page-header { margin-bottom: 20px; font-size: 14px; color: #666; }
.material-group { margin-bottom: 40px; padding-bottom: 20px; border-bottom: none; }
.material-group-title { font-size: 20px; font-weight: bold; margin-bottom: 20px; color: #333; }
.option-item { display: flex; align-items: flex-start; margin-bottom: 8px;}
.option-letter { margin-right: 8px; min-width: 20px;}
.option-content { flex: 1;}
.material-group.single-question .question { border-bottom: none; }
.material-group.single-question::after { content: ""; display: block; width: 100%; height: 1px; background-color: #eee; margin-top: 20px; }

`;
            head.appendChild(style);

            // 创建body元素
            const body = doc.createElement('body');
            html.appendChild(body);

            // 创建内容容器
            const container = doc.createElement('div');
            container.className = 'container';
            container.style.display = 'none';
            body.appendChild(container);

            doc.close();
            return doc;
        };

        // 6. 初始化页面并加载依赖
        const init = () => {
            const doc = buildBasicDOM();
            const container = doc.querySelector('.container');

            // 检查浏览器支持
            const checkBrowserSupport = () => {
                if (!window.Promise) {
                    throw new Error('您的浏览器不支持Promise，无法使用此功能');
                }
                if (!window.Blob) {
                    throw new Error('您的浏览器不支持Blob，无法导出PDF');
                }
                if (!window.URL) {
                    throw new Error('您的浏览器不支持URL API，无法导出PDF');
                }
            };

            try {
                checkBrowserSupport();
            } catch (e) {
                alert(e.message);
                return;
            }

            // 依赖加载完成后执行的函数
            const doShow = () => {
                // 清空容器并填充内容
                container.innerHTML = '';

                // 1. 创建头部（只保留导出按钮）
                const header = doc.createElement('div');
                header.className = 'header';

                // 创建导出按钮
                const exportBtn = doc.createElement('button');
                exportBtn.className = 'export-btn';
                exportBtn.id = 'export-pdf';

                // 创建导出按钮SVG图标
                const svg = doc.createElementNS('http://www.w3.org/2000/svg', 'svg');
                svg.setAttribute('width', '16');
                svg.setAttribute('height', '16');
                svg.setAttribute('viewBox', '0 0 24 24');
                svg.setAttribute('fill', 'none');
                svg.setAttribute('stroke', 'currentColor');
                svg.setAttribute('stroke-width', '2');

                const path1 = doc.createElementNS('http://www.w3.org/2000/svg', 'path');
                path1.setAttribute('d', 'M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z');
                svg.appendChild(path1);

                const path2 = doc.createElementNS('http://www.w3.org/2000/svg', 'polyline');
                path2.setAttribute('points', '14 2 14 8 20 8');
                svg.appendChild(path2);

                const path3 = doc.createElementNS('http://www.w3.org/2000/svg', 'line');
                path3.setAttribute('x1', '16');
                path3.setAttribute('y1', '13');
                path3.setAttribute('x2', '8');
                path3.setAttribute('y2', '13');
                svg.appendChild(path3);

                const path4 = doc.createElementNS('http://www.w3.org/2000/svg', 'line');
                path4.setAttribute('x1', '16');
                path4.setAttribute('y1', '17');
                path4.setAttribute('x2', '8');
                path4.setAttribute('y2', '17');
                svg.appendChild(path4);

                const path5 = doc.createElementNS('http://www.w3.org/2000/svg', 'polyline');
                path5.setAttribute('points', '10 9 9 9 8 9');
                svg.appendChild(path5);

                exportBtn.appendChild(svg);
                exportBtn.appendChild(doc.createTextNode(' 导出为PDF'));
                header.appendChild(exportBtn);

                container.appendChild(header);

                // 2. 添加导出选项
                const exportOptions = doc.createElement('div');
                exportOptions.className = 'export-options';

                // 检查是否有错题数据
                const hasWrongQuestions = this.state.globalWrongQuestionIds &&
                    Array.isArray(this.state.globalWrongQuestionIds) &&
                    this.state.globalWrongQuestionIds.length > 0;

                // 筛选出在当前试卷中的错题
                const wrongQuestionIdsInCurrent = hasWrongQuestions
                    ? this.state.globalWrongQuestionIds.filter(id =>
                        solutions.some(s => s.key === id)
                    )
                    : [];

                // 检查是否有错题数据
                const hasUnAsweredQuestions = this.state.globalUnAsweredQuestionIds &&
                    Array.isArray(this.state.globalUnAsweredQuestionIds) &&
                    this.state.globalUnAsweredQuestionIds.length > 0;

                // 筛选出在当前试卷中的错题
                const unAnsweredQuestionIdsInCurrent = hasUnAsweredQuestions
                    ? this.state.globalUnAsweredQuestionIds.filter(id =>
                        solutions.some(s => s.key === id)
                    )
                    : [];


                // 构建选项HTML
                exportOptions.innerHTML = `
                <div class="export-option-item">
                    <input type="radio" id="export-all" name="export-type" value="all" checked>
                    <label for="export-all" class="export-option-label">导出全部题目 (${solutions.length}题)</label>
                </div>
                <div class="export-option-item">
                    <input type="radio" id="export-wrong" name="export-type" value="wrong" ${!hasWrongQuestions ? 'disabled' : ''}>
                    <label for="export-wrong" class="export-option-label">仅导出错题 (${wrongQuestionIdsInCurrent.length}题)</label>
                </div>
                ${!hasWrongQuestions ? '<div class="no-wrong-questions">没有检测到错题数据</div>' : ''}
                  <div class="export-option-item">
                    <input type="radio" id="export-unanswered" name="export-type" value="unanswered" ${!hasUnAsweredQuestions ? 'disabled' : ''}>
                    <label for="export-unanswered" class="export-option-label">仅导出未作答题 (${unAnsweredQuestionIdsInCurrent.length}题)</label>
                </div>
                ${!hasUnAsweredQuestions ? '<div class="no-unanswered-questions">没有检测到未作答题目数据</div>' : ''}
            `;

                container.appendChild(exportOptions);

                // 3. 创建题目容器
                const solutionsContainer = doc.createElement('div');
                solutionsContainer.id = 'solutions-container';
                container.appendChild(solutionsContainer);

                // 4. 按材料组渲染题目
                let questionIndex = 0; // 全局题目索引，用于显示正确的题号
                groupedByMaterial.forEach((materialGroup, groupIndex) => {
                    const groupDiv = doc.createElement('div');
                    groupDiv.className = 'material-group';
                    groupDiv.dataset.groupIndex = groupIndex;
                    groupDiv.dataset.hasMaterial = materialGroup.hasMaterial;

                    // ===== 新增代码开始 =====
                    // 判断当前材料组的题目数量，添加对应类名
                    const questionCount = materialGroup.questions.length;
                    if (questionCount === 1) {
                        groupDiv.classList.add('single-question'); // 单题：加single-question类
                    } else {
                        groupDiv.classList.add('multi-question'); // 多题：加multi-question类
                    }
                    // ===== 新增代码结束 =====

                    const materialKey = Array.from(materialMap.entries())
                        .find(([_, value]) => value === materialGroup)?.[0];

                    if (materialKey) {
                        groupDiv.dataset.materialKey = materialKey;
                    }

                    // 材料组标题
                    const groupTitle = doc.createElement('div');
                    groupTitle.className = 'material-group-title';
                    if (materialGroup.material) {
                        groupTitle.textContent = `材料组 ${groupIndex + 1} (包含 ${materialGroup.questions.length} 题)`
                    }
                    groupDiv.appendChild(groupTitle);

                    // 材料部分（如有）
                    if (exportStore.exportOptions.includeMaterial && materialGroup.material) {
                        const materialDiv = doc.createElement('div');
                        materialDiv.className = 'material';
                        materialDiv.dataset.section = 'material';
                        materialDiv.dataset.groupIndex = groupIndex;

                        const materialTitle = doc.createElement('div');
                        materialTitle.className = 'material-title';
                        materialTitle.textContent = '材料：';
                        materialDiv.appendChild(materialTitle);

                        const materialContent = doc.createElement('div');
                        materialContent.className = 'material-content';
                        materialContent.innerHTML = materialGroup.material;
                        materialDiv.appendChild(materialContent);

                        groupDiv.appendChild(materialDiv);
                    }

                    // 渲染当前材料组下的所有题目
                    materialGroup.questions.forEach((item) => {
                        questionIndex++;

                        const questionDiv = doc.createElement('div');
                        questionDiv.className = 'question';
                        questionDiv.dataset.section = 'question';
                        questionDiv.dataset.questionIndex = questionIndex;
                        questionDiv.dataset.id = item.key;
                        questionDiv.dataset.groupIndex = groupIndex;

                        // 错题标记
                        const isWrongQuestion = hasWrongQuestions &&
                            wrongQuestionIdsInCurrent.includes(item.key);

                        if (isWrongQuestion) {
                            questionDiv.style.borderLeft = '4px solid #ef4444';
                            questionDiv.style.paddingLeft = '15px';
                        }

                        questionDiv.style.display = 'block';

                        // 题目编号
                        const questionNumber = doc.createElement('div');
                        questionNumber.className = 'question-number';
                        questionNumber.textContent = `第 ${questionIndex} 题${isWrongQuestion ? ' (错题)' : ''}`;
                        questionDiv.appendChild(questionNumber);

                        // 题目内容
                        const contentDiv = doc.createElement('div');
                        contentDiv.className = 'content';
                        contentDiv.dataset.section = 'content';

                        const contentTitle = doc.createElement('div');
                        contentTitle.className = 'content-title';
                        contentTitle.textContent = '题目：';
                        //contentDiv.appendChild(contentTitle);

                        // ===== 新增代码开始 =====
                        // 1. 创建题目类型标识元素
                        const typeLabel = doc.createElement('span');
                        typeLabel.className = 'question-type-label';
                        console.log('题目类型：', item.type);

                        // 2. 判断type值，显示对应文本
                        if (item.type == 1) {
                            typeLabel.textContent = `【单选题】${questionIndex}.`;
                            typeLabel.style.color = '#4F46E5'; // 单选-紫色
                            typeLabel.style.fontWeight = 'bold'; // 直接加行内样式（兜底） 
                        } else if (item.type == 2) {
                            typeLabel.textContent = `【多选题】${questionIndex}.`;
                            typeLabel.style.color = '#ef4444'; // 多选-红色
                            typeLabel.style.fontWeight = 'bold'; // 直接加行内样式（兜底）
                        } else if (item.type == 5) {
                            typeLabel.textContent = `【判断题】${questionIndex}.`;
                            typeLabel.style.color = '#ce8722'; // 判断-棕色
                            typeLabel.style.fontWeight = 'bold'; // 直接加行内样式（兜底）
                        }

                        // 核心修改：先创建行内容器，把标识和题目内容放在一起，避免换行
                        const contentText = doc.createElement('div');
                        contentText.className = 'content-text';

                        // 先清空默认内容，避免干扰
                        contentText.innerHTML = '';
                        // 第一步：添加类型标识（行内元素）
                        contentText.appendChild(typeLabel);

                        // 第二步：添加空格分隔标识和题目
                        contentText.appendChild(doc.createTextNode(' '));

                        // 第三步：处理题目内容（关键：把HTML内容转成行内文本/行内元素，避免换行）
                        const questionContent = document.createElement('span');
                        // 去除题目内容中的<p>标签（这是导致换行的核心原因）
                        let pureContent = item.content.replace(/<p>/g, '').replace(/<\/p>/g, '');
                        questionContent.innerHTML = pureContent;
                        contentText.appendChild(questionContent);

                        // 后续原有逻辑不变
                        contentDiv.appendChild(contentText);
                        questionDiv.appendChild(contentDiv);

                        // 选项部分 - 关键修改：判断题强制渲染选项，不再依赖item.options
                        const shouldShowOptions = exportStore.exportOptions.includeOptions;
                        const hasValidOptions = item.options && Array.isArray(item.options) && item.options.length > 0;
                        // 判断题强制显示选项，不管原数据有没有
                        const isJudgeQuestion = item.type === 5;

                        if (shouldShowOptions && (hasValidOptions || isJudgeQuestion)) {
                            const optionsDiv = doc.createElement('div');
                            optionsDiv.className = 'options';
                            optionsDiv.dataset.section = 'options';

                            const optionsText = doc.createElement('div');
                            optionsText.className = 'options-text';

                            const optionLetters = ['A', 'B', 'C', 'D'];
                            let displayOptions;

                            if (isJudgeQuestion) {
                                // 判断题：固定用正确/错误，无视原数据
                                displayOptions = ['正确', '错误'];
                            } else {
                                // 其他题型：用原选项
                                displayOptions = item.options;
                            }

                            displayOptions.forEach((option, index) => {
                                if (index < 4) {
                                    const optionItem = doc.createElement('div');
                                    optionItem.className = 'option-item';

                                    const letterSpan = doc.createElement('span');
                                    letterSpan.className = 'option-letter';
                                    letterSpan.textContent = `${optionLetters[index]}：`;

                                    const contentContainer = doc.createElement('div');
                                    contentContainer.className = 'option-content';

                                    if (typeof option === 'string') {
                                        let processedOption = option.replace(/^<p>/, '').replace(/<\/p>$/, '');
                                        contentContainer.innerHTML = processedOption;
                                    } else {
                                        contentContainer.textContent = option;
                                    }

                                    optionItem.appendChild(letterSpan);
                                    optionItem.appendChild(contentContainer);
                                    optionsText.appendChild(optionItem);
                                }
                            });

                            optionsDiv.appendChild(optionsText);
                            questionDiv.appendChild(optionsDiv);
                        }
                        // 建立索引到选项字母的映射关系
                        const optionLetters = ['A', 'B', 'C', 'D'];
                        // 检查item.correctAnswer存在且包含choice属性
                        if (exportStore.exportOptions.includeSolution && item.correctAnswer && 'choice' in item.correctAnswer) {
                            // 获取正确选项的原始值（可能是单个数字/逗号分隔字符串）
                            let correctAnswerRaw = item.correctAnswer.choice;
                            let correctAnswerLetters = [];

                            // ===== 核心兼容逻辑 =====
                            if (typeof correctAnswerRaw === 'string') {
                                // 多选场景：逗号分隔的字符串（如 "0,1,2"）
                                const indexArray = correctAnswerRaw.split(',').map(item => parseInt(item.trim()));
                                // 过滤有效索引（0-3）并转成字母
                                correctAnswerLetters = indexArray.filter(index =>
                                    !isNaN(index) && index >= 0 && index < optionLetters.length
                                ).map(index => optionLetters[index]);
                            } else if (typeof correctAnswerRaw === 'number') {
                                // 单选场景：单个数字（如 0）
                                if (correctAnswerRaw >= 0 && correctAnswerRaw < optionLetters.length) {
                                    correctAnswerLetters = [optionLetters[correctAnswerRaw]];
                                }
                            }

                            // 只有有有效答案时才渲染
                            if (correctAnswerLetters.length > 0) {
                                const correctDiv = doc.createElement('div');
                                correctDiv.className = 'correct';
                                correctDiv.dataset.section = 'correct';

                                const correctTitle = doc.createElement('div');
                                correctTitle.className = 'correct-title';
                                correctTitle.textContent = '正确答案：';
                                correctDiv.appendChild(correctTitle);

                                const correctText = doc.createElement('div');
                                correctText.className = 'correct-text';
                                // 多选拼接成 "A、B、C"，单选就是 "A"
                                correctText.innerHTML = correctAnswerLetters.join('、');
                                correctDiv.appendChild(correctText);

                                questionDiv.appendChild(correctDiv);
                            }
                        }
                        if (exportStore.exportOptions.includeSolution && item.correctRatio && item.correctRatio > 0) {
                            const correctRatioDiv = doc.createElement('div');
                            correctRatioDiv.className = 'correct-ratio';
                            correctRatioDiv.dataset.section = 'correct-ratio';

                            const correctRatioTitle = doc.createElement('div');
                            correctRatioTitle.className = 'correct-ratio-title';
                            correctRatioTitle.textContent = '全站准确率：';
                            correctRatioDiv.appendChild(correctRatioTitle);

                            const correctRatioText = doc.createElement('div');
                            correctRatioText.className = 'correct-ratio-text';
                            correctRatioText.innerHTML = item.correctRatio.toFixed(2) + '%';
                            correctRatioDiv.appendChild(correctRatioText);
                            questionDiv.appendChild(correctRatioDiv);
                        }

                        // 检查item.mostWrongAnswer存在且包含choice属性
                        if (exportStore.exportOptions.includeSolution && item.mostWrongAnswer && 'choice' in item.mostWrongAnswer) {
                            // 获取错误选项的索引值
                            const wrongChoiceIndex = item.mostWrongAnswer.choice;

                            if (wrongChoiceIndex >= 0 && wrongChoiceIndex < optionLetters.length) {
                                const wrongChoiceLetter = optionLetters[wrongChoiceIndex];
                                const choiceDiv = doc.createElement('div');
                                choiceDiv.className = 'choice';
                                choiceDiv.dataset.section = 'choice';

                                const choiceTitle = doc.createElement('div');
                                choiceTitle.className = 'choice-title';
                                choiceTitle.textContent = '易错项：';
                                choiceDiv.appendChild(choiceTitle);

                                const choiceText = doc.createElement('div');
                                choiceText.className = 'choice-text';
                                choiceText.innerHTML = wrongChoiceLetter;
                                choiceDiv.appendChild(choiceText);

                                questionDiv.appendChild(choiceDiv);
                            }
                        }
                        const solutionDiv = doc.createElement('div');
                        // 解析内容
                        if (exportStore.exportOptions.includeSolution && item.solution) {

                            solutionDiv.className = 'solution';
                            solutionDiv.dataset.section = 'solution';

                            const solutionTitle = doc.createElement('div');
                            solutionTitle.className = 'solution-title';
                            solutionTitle.textContent = '解析：';
                            solutionDiv.appendChild(solutionTitle);

                            const solutionText = doc.createElement('div');
                            solutionText.className = 'solution-text';
                            solutionText.innerHTML = item.solution;
                            solutionDiv.appendChild(solutionText);

                            questionDiv.appendChild(solutionDiv);
                        }

                        //来源
                        if (exportStore.exportOptions.includeSolution && item.source) {
                            const sourceDiv = doc.createElement('div');
                            sourceDiv.className = 'source';
                            sourceDiv.dataset.section = 'source';

                            const sourceTitle = doc.createElement('div');
                            sourceTitle.className = 'source-title';
                            sourceTitle.textContent = '来源：';
                            sourceDiv.appendChild(sourceTitle);

                            const sourceText = doc.createElement('div');
                            sourceText.className = 'source-text';
                            sourceText.innerHTML = item.source;
                            sourceDiv.appendChild(sourceText);

                            solutionDiv.appendChild(sourceDiv);
                        }

                        groupDiv.appendChild(questionDiv);
                    });

                    solutionsContainer.appendChild(groupDiv);
                });

                // 计算总页数：精确控制分页逻辑
                exportStore.totalPages = groupedByMaterial.reduce((total, group) => {
                    const materialPages = group.hasMaterial ? 1 : 0;
                    const questionPages = group.hasMaterial && includeSolution
                        ? group.questions.length * 2  // 有材料：每题2页（题目+解析）
                        : group.questions.length * 1; // 无材料：每题1页（题目+解析）
                    return total + materialPages + questionPages;
                }, 0);

                // 5. 添加交互功能（导出）
                addInteraction(solutionWindow, groupedByMaterial, wrongQuestionIdsInCurrent, unAnsweredQuestionIdsInCurrent, paperName, exportStore, materialMap);

                // 6. 隐藏加载提示，显示内容
                container.style.display = 'block';
            };

            // 显示内容
            doShow();

        };

        // 7. 添加交互功能（PDF导出）
        const addInteraction = (win, materialGroups, wrongQuestionIds, unAnsweredQuestionIds, paperName, exportStore, materialMap) => {
            const doc = win.document;
            const questions = doc.querySelectorAll('.question');
            const groups = doc.querySelectorAll('.material-group');
            const container = doc.querySelector('.container');
            const exportBtn = doc.getElementById('export-pdf');
            const exportTypeRadios = doc.querySelectorAll('input[name="export-type"]');
            let name = "题目";

            // 处理文件名特殊字符
            function getPdfFileName() {
                // 添加标题
                if (includeSolution) {
                    paperName = paperName.replace(/[\/:*?"<>|]/g, '-') + '_' + name + '解析.pdf'
                } else {
                    paperName = paperName.replace(/[\/:*?"<>|]/g, '-');
                }
                return paperName;
            }

            // 根据导出类型筛选要导出的题目组和题目
            function getFilteredGroups() {
                const exportType = exportStore.exportOptions.exportType;

                // 如果不是错题也不是未作答，则返回所有题目组
                if (exportType !== 'wrong' && exportType !== 'unanswered') {
                    return [...materialGroups];
                }

                return materialGroups.map(group => {
                    let filteredQuestions;

                    // 根据导出类型筛选题目
                    if (exportType === 'wrong') {
                        // 筛选错题
                        filteredQuestions = group.questions.filter(
                            q => wrongQuestionIds.includes(Number(q.key))
                        );
                        name = "错题";
                    } else {
                        // 筛选未作答题目（假设存在未作答题目ID数组unansweredQuestionIds）
                        filteredQuestions = group.questions.filter(
                            q => unAnsweredQuestionIds.includes(Number(q.key))
                        );
                        name = "未作答题目";
                    }

                    return {
                        ...group,
                        questions: filteredQuestions
                    };
                }).filter(group => group.questions.length > 0); // 过滤掉没有符合条件题目的组
            }

            function updateDisplayByExportType(exportType) {
                const isExportWrong = exportType === 'wrong';
                const isExportUnanswered = exportType === 'unanswered';

                // 1. 控制每个题目是否显示
                questions.forEach(q => {
                    const questionId = q.dataset.id;
                    const isWrong = wrongQuestionIds.includes(Number(questionId));
                    // 假设存在未作答题目ID的数组unansweredQuestionIds
                    const isUnanswered = unAnsweredQuestionIds.includes(Number(questionId));

                    // 根据不同类型显示对应的题目
                    if (isExportWrong) {
                        q.style.display = isWrong ? 'block' : 'none';
                    } else if (isExportUnanswered) {
                        q.style.display = isUnanswered ? 'block' : 'none';
                    } else {
                        // 默认显示所有题目
                        q.style.display = 'block';
                    }
                });

                // 2. 控制每个 group 是否显示，并动态更新标题中的数量
                groups.forEach(group => {
                    const groupQuestions = group.querySelectorAll('.question');
                    const visibleQuestions = Array.from(groupQuestions).filter(q => q.style.display !== 'none');
                    const hasVisibleQuestions = visibleQuestions.length > 0;
                    group.style.display = hasVisibleQuestions ? 'block' : 'none';

                    if (hasVisibleQuestions && (isExportWrong || isExportUnanswered)) {
                        // 统计当前显示的题目数量（错题或未答题目）
                        let visibleCount = 0;
                        visibleQuestions.forEach(q => {
                            const questionId = q.dataset.id;
                            if ((isExportWrong && wrongQuestionIds.includes(Number(questionId))) ||
                                (isExportUnanswered && unAnsweredQuestionIds.includes(Number(questionId)))) {
                                visibleCount++;
                            }
                        });

                        const materialKey = group.getAttribute('data-material-key');
                        if (!materialKey.includes('no')) {
                            // 找到当前 group 的标题并更新，根据类型显示不同文本
                            const groupTitleEl = group.querySelector('.material-group-title');
                            if (groupTitleEl) {
                                if (isExportWrong) {
                                    groupTitleEl.textContent = `材料组 (包含 ${visibleCount} 错题)`;
                                } else if (isExportUnanswered) {
                                    groupTitleEl.textContent = `材料组 (包含 ${visibleCount} 未答题目)`;
                                }
                            }
                        }
                    }
                });
            }

            // 监听导出类型变化
            exportTypeRadios.forEach(radio => {
                radio.addEventListener('change', () => {
                    if (radio.checked) {
                        exportStore.exportOptions.exportType = radio.value;
                        updateDisplayByExportType(radio.value);
                    }
                });
            });

            // 重置所有部分的显示状态
            function resetSectionVisibility() {
                const sections = doc.querySelectorAll('[data-section]');
                sections.forEach(section => {
                    section.classList.remove('hide-section');
                });
            }

            // 隐藏指定部分
            function hideSections(sectionsToHide) {
                resetSectionVisibility();
                sectionsToHide.forEach(section => {
                    const elements = doc.querySelectorAll(`[data-section="${section}"]`);
                    elements.forEach(el => el.classList.add('hide-section'));
                });
            }

            // 只显示特定组
            function showOnlyGroup(groupIndex) {
                groups.forEach((group, idx) => {
                    group.style.display = idx === groupIndex ? 'block' : 'none';
                });
            }

            // 只显示特定题目
            function showOnlyQuestion(questionId) {
                questions.forEach(q => {
                    q.style.display = Number(q.dataset.id) === Number(questionId) ? 'block' : 'none';
                });
            }

            function getGroupElementByIndex(filteredGroups, groupIndex) {
                try {
                    const originalGroup = filteredGroups[groupIndex];
                    if (!originalGroup) {
                        console.error(`找不到索引为${groupIndex}的组`);
                        return null;
                    }

                    // 重点修复：无材料组的匹配逻辑
                    if (!originalGroup.hasMaterial) {
                        // 1. 先找DOM中标记为无材料的组
                        const candidateGroups = doc.querySelectorAll('.material-group[data-has-material="false"]');

                        // 2. 通过组内题目ID进行匹配（最可靠的方式）
                        const groupQuestionIds = originalGroup.questions.map(q => q.key.toString());

                        for (const candidate of candidateGroups) {
                            // 获取候选组中的所有题目ID
                            const candidateQuestionIds = Array.from(candidate.querySelectorAll('.question'))
                                .map(q => q.dataset.id);

                            // 检查是否有共同的题目ID（证明是同一个组）
                            const isMatch = groupQuestionIds.some(id =>
                                candidateQuestionIds.includes(id)
                            );

                            if (isMatch) {
                                return candidate; // 找到匹配的组
                            }
                        }

                        // 3. 兜底方案：使用组索引查找
                        return doc.querySelector(`.material-group[data-group-index="${groupIndex}"]`);
                    }

                    // 有材料的组保持原逻辑
                    const entries = Array.from(materialMap.entries());

                    const foundEntry = entries.find(([key, value]) => key === originalGroup.materialKey);


                    if (!foundEntry) {
                        console.error(`找不到与组匹配的 materialMap 条目:`, originalGroup);
                        return doc.querySelector(`.material-group[data-group-index="${groupIndex}"]`);
                    }

                    const [materialKey] = foundEntry;
                    const groupElement = doc.querySelector(`.material-group[data-material-key="${materialKey}"]`);

                    if (!groupElement) {
                        console.warn(`找不到materialKey为${materialKey}的组元素，使用索引查找`);
                        return doc.querySelector(`.material-group[data-group-index="${groupIndex}"]`);
                    }

                    return groupElement;
                } catch (error) {
                    console.error('获取组元素时发生错误:', error);
                    return doc.querySelector(`.material-group[data-group-index="${groupIndex}"]`);
                }
            }


            // PDF导出功能实现 - 修复空白页和错题导出问题
            const exportToPDF = async () => {

                if (exportStore.isExporting) return;

                exportStore.isExporting = true;
                //exportBtn.disabled = true;
                //exportBtn.innerHTML = '<div class="spinner" style="width: 16px; height: 16px; margin-right: 5px;"></div> 正在导出...';
                exportBtn.style.display = 'none'; // 直接隐藏按钮
                // 隐藏导出选项卡
                const exportOptionsEl = doc.querySelector('.export-options');
                const originalExportOptionsDisplay = exportOptionsEl.style.display;
                exportOptionsEl.style.display = 'none';

                // 获取过滤后的组
                const filteredGroups = getFilteredGroups();

                if (filteredGroups.length === 0) {
                    solutionWindow.alert('没有可导出的题目，请选择其他导出类型');
                    exportStore.isExporting = false;
                    exportOptionsEl.style.display = originalExportOptionsDisplay;
                    exportBtn.style.display = ''; // 直接显示按钮
                    //exportBtn.innerHTML = '<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg> 导出为PDF';
                    return;
                }

                // 计算过滤后的总页数（关键：与实际生成页数严格一致）
                const totalPages = filteredGroups.reduce((total, group) => {
                    const materialPages = group.hasMaterial ? 1 : 0;
                    const questionPages = group.hasMaterial && includeSolution ? group.questions.length * 2 : group.questions.length * 1;
                    return total + materialPages + questionPages;
                }, 0);

                // 创建导出进度提示
                const loading = doc.createElement('div');
                loading.className = 'loading';
                loading.innerHTML = `
                <div class="spinner"></div>
                <div>正在生成PDF，第 <span id="current-page">1</span>/${totalPages} 页</div>
                <div class="progress-container">
                    <div class="progress-bar">
                        <div class="progress-fill" id="export-progress"></div>
                    </div>
                </div>
            `;
                doc.body.appendChild(loading);
                const progressFill = doc.getElementById('export-progress');
                const currentPageEl = doc.getElementById('current-page');

                try {
                    // 准备导出环境
                    container.classList.add('export-preview');
                    win.scrollTo(0, 0);
                    await new Promise(resolve => setTimeout(resolve, 500));

                    // 创建PDF实例
                    const { jsPDF } = jspdf;
                    const pdf = new jsPDF('p', 'mm', 'a4');

                    // 设置页面尺寸
                    const pageWidth = 210;
                    const pageHeight = 297;
                    const margin = 15;
                    const contentWidth = pageWidth - margin * 2;
                    let currentGlobalPage = 1; // 从1开始计数，与PDF页码一致

                    // 遍历每个过滤后的材料组
                    for (let groupIndex = 0; groupIndex < filteredGroups.length; groupIndex++) {
                        const group = filteredGroups[groupIndex];
                        const groupElement = getGroupElementByIndex(filteredGroups, groupIndex);
                        // 检查组元素是否有效
                        if (!groupElement || group.questions.length === 0) {
                            console.warn(`跳过无效的组，索引: ${groupIndex}`);
                            continue;
                        }

                        // 只显示当前组
                        showOnlyGroup(parseInt(groupElement.dataset.groupIndex));

                        // 1. 导出材料页（如果有材料）
                        if (group.hasMaterial && group.material) {
                            // 仅在不是第一页时添加新页面
                            if (currentGlobalPage > 1) {
                                pdf.addPage();
                            }

                            // 隐藏题目选项和解析
                            hideSections(['question', 'options', 'solution']);

                            // 添加页面标题
                            const pageHeader = doc.createElement('div');
                            pageHeader.className = 'page-header';
                            pageHeader.textContent = `材料组 ${groupIndex + 1} - 材料部分`;
                            groupElement.insertBefore(pageHeader, groupElement.firstChild);

                            // 等待渲染
                            await new Promise(resolve => setTimeout(resolve, 300));

                            // 截图并添加到PDF
                            const canvas = await html2canvas(container, {
                                scale: 2,
                                logging: false,
                                scrollX: 0,
                                scrollY: 0,
                                useCORS: true,
                                allowTaint: true,
                                windowWidth: container.offsetWidth,
                                windowHeight: container.offsetHeight
                            });

                            const imgData = canvas.toDataURL('image/jpeg', exportStore.exportOptions.quality);
                            const imgHeight = canvas.height * contentWidth / canvas.width;
                            const finalHeight = imgHeight > pageHeight - margin * 2
                                ? pageHeight - margin * 2
                                : imgHeight;

                            pdf.addImage(imgData, 'JPEG', margin, margin, contentWidth, finalHeight);
                            // 添加页码
                            pdf.setFontSize(10);
                            pdf.text(`${currentGlobalPage}/${totalPages}`,
                                pageWidth - margin - 40,
                                pageHeight - margin);

                            // 移除临时标题
                            groupElement.removeChild(pageHeader);

                            currentGlobalPage++;
                            progressFill.style.width = `${((currentGlobalPage - 1) / totalPages) * 100}%`;
                            currentPageEl.textContent = currentGlobalPage;
                        }

                        // 2. 导出当前组的所有题目
                        for (let qIndex = 0; qIndex < group.questions.length; qIndex++) {
                            const question = group.questions[qIndex];
                            const questionElement = doc.querySelector(`.question[data-id="${question.key}"]`);

                            if (!questionElement) continue;

                            // 只显示当前题目
                            showOnlyQuestion(question.key);

                            // 有材料的组：题目和解析分开显示；无材料的组：题目和解析在同一页
                            if (group.hasMaterial) {
                                // 隐藏材料和解析，只显示题目和选项
                                hideSections(['material', 'solution', 'source', 'choice', 'correct', 'correct-ratio']);

                                // 添加页面标题
                                const pageHeader = doc.createElement('div');
                                pageHeader.className = 'page-header';
                                pageHeader.textContent = `材料组 ${groupIndex + 1} - 第 ${questionElement.dataset.questionIndex} 题（题目与选项）`;
                                questionElement.insertBefore(pageHeader, questionElement.firstChild);

                                // 等待渲染
                                await new Promise(resolve => setTimeout(resolve, 300));

                                // 截图并添加到PDF
                                const canvas = await html2canvas(container, {
                                    scale: 2,
                                    logging: false,
                                    scrollX: 0,
                                    scrollY: 0,
                                    useCORS: true,
                                    allowTaint: true
                                });

                                const imgData = canvas.toDataURL('image/jpeg', exportStore.exportOptions.quality);
                                const imgHeight = canvas.height * contentWidth / canvas.width;
                                const finalHeight = imgHeight > pageHeight - margin * 2
                                    ? pageHeight - margin * 2
                                    : imgHeight;

                                // 添加新页面（关键：只在需要时添加）
                                if (currentGlobalPage > 1) {
                                    pdf.addPage();
                                }
                                pdf.addImage(imgData, 'JPEG', margin, margin, contentWidth, finalHeight);
                                // 添加页码
                                pdf.setFontSize(10);
                                pdf.text(`${currentGlobalPage}/${totalPages}`,
                                    pageWidth - margin - 40,
                                    pageHeight - margin);

                                // 移除临时标题
                                questionElement.removeChild(pageHeader);

                                currentGlobalPage++;
                                progressFill.style.width = `${((currentGlobalPage - 1) / totalPages) * 100}%`;
                                currentPageEl.textContent = currentGlobalPage;

                                // 3. 导出当前题目的解析（只有有材料的组才单独导出解析页）
                                // 解析内容
                                if (exportStore.exportOptions.includeSolution) {
                                    // 隐藏材料和选项，只显示解析
                                    hideSections(['material', 'content', 'options']);

                                    // 添加页面标题
                                    const solutionHeader = doc.createElement('div');
                                    solutionHeader.className = 'page-header';
                                    solutionHeader.textContent = `材料组 ${groupIndex + 1} - 第 ${questionElement.dataset.questionIndex} 题（解析）`;
                                    questionElement.insertBefore(solutionHeader, questionElement.firstChild);

                                    // 等待渲染
                                    await new Promise(resolve => setTimeout(resolve, 500));

                                    // 截图并添加到PDF
                                    const solutionCanvas = await html2canvas(container, {
                                        scale: 2,
                                        logging: false,
                                        scrollX: 0,
                                        scrollY: 0,
                                        useCORS: true,
                                        allowTaint: true
                                    });

                                    const solutionImgData = solutionCanvas.toDataURL('image/jpeg', exportStore.exportOptions.quality);
                                    const solutionImgHeight = solutionCanvas.height * contentWidth / solutionCanvas.width;
                                    const solutionFinalHeight = solutionImgHeight > pageHeight - margin * 2
                                        ? pageHeight - margin * 2
                                        : solutionImgHeight;

                                    // 添加新页面
                                    pdf.addPage();
                                    pdf.addImage(solutionImgData, 'JPEG', margin, margin, contentWidth, solutionFinalHeight);
                                    // 添加页码
                                    pdf.setFontSize(10);
                                    pdf.text(`${currentGlobalPage}/${totalPages}`,
                                        pageWidth - margin - 40,
                                        pageHeight - margin);

                                    // 移除临时标题
                                    questionElement.removeChild(solutionHeader);

                                    currentGlobalPage++;
                                    progressFill.style.width = `${((currentGlobalPage - 1) / totalPages) * 100}%`;
                                    currentPageEl.textContent = currentGlobalPage;
                                }
                            } else {
                                // 无材料的组：题目和解析在同一页
                                hideSections(['material']); // 只隐藏材料，保留其他内容

                                // 等待渲染
                                await new Promise(resolve => setTimeout(resolve, 500));

                                // 截图并添加到PDF
                                const canvas = await html2canvas(container, {
                                    scale: 2,
                                    logging: false,
                                    scrollX: 0,
                                    scrollY: 0,
                                    useCORS: true,
                                    allowTaint: true
                                });

                                const imgData = canvas.toDataURL('image/jpeg', exportStore.exportOptions.quality);
                                const imgHeight = canvas.height * contentWidth / canvas.width;
                                const finalHeight = imgHeight > pageHeight - margin * 2
                                    ? pageHeight - margin * 2
                                    : imgHeight;

                                // 仅在不是第一页时添加新页面（避免空白页）
                                if (currentGlobalPage > 1) {
                                    pdf.addPage();
                                }
                                pdf.addImage(imgData, 'JPEG', margin, margin, contentWidth, finalHeight);
                                // 添加页码
                                pdf.setFontSize(10);
                                pdf.text(`${currentGlobalPage}/${totalPages}`,
                                    pageWidth - margin - 40,
                                    pageHeight - margin);

                                currentGlobalPage++;
                                progressFill.style.width = `${((currentGlobalPage - 1) / totalPages) * 100}%`;
                                currentPageEl.textContent = currentGlobalPage;
                            }
                        }
                    }

                    // 保存PDF文件
                    pdf.save(getPdfFileName());
                    const totalQuestions = filteredGroups.reduce((sum, group) => sum + group.questions.length, 0);
                    solutionWindow.alert(`成功导出 ${totalQuestions} 道题目到PDF！总页数: ${totalPages}`);

                } catch (error) {
                    console.error('PDF导出错误：', error);
                    console.error(error.message);
                    let errorMsg = 'PDF导出失败：';
                    if (error.message.includes('html2canvas')) {
                        errorMsg += '页面截图工具加载失败，请重试或更换浏览器';
                    } else if (error.message.includes('jsPDF')) {
                        errorMsg += 'PDF生成工具加载失败，请重试';
                    } else if (error.message.includes('timeout')) {
                        errorMsg += '操作超时，请重试';
                    } else {
                        errorMsg += error.message;
                    }
                    solutionWindow.alert(errorMsg);
                } finally {
                    // 恢复页面状态
                    // 恢复导出选项卡显示
                    exportOptionsEl.style.display = originalExportOptionsDisplay;
                    container.classList.remove('export-preview');
                    resetSectionVisibility();
                    updateDisplayByExportType(exportStore.exportOptions.exportType);
                    doc.body.removeChild(loading);
                    exportStore.isExporting = false;
                    //exportBtn.disabled = false;
                    //exportBtn.innerHTML = '<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg> 导出为PDF';
                    exportBtn.style.display = ''; // 直接显示按钮
                }
            };


            const checkLib = () => {
                // 定义需要加载的脚本及其检查条件
                const scripts = [
                    {
                        id: 'jspdf',
                        src: 'https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.1.1/jspdf.umd.min.js',
                        check: () => typeof window.jspdf !== 'undefined',
                        loadedMsg: 'pdf所需js依赖已加载',
                        loadingMsg: '正在引入pdf所需js依赖',
                        errorMsg: 'jspdf加载失败'
                    },
                    {
                        id: 'html2canvas',
                        src: 'https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js',
                        check: () => typeof window.html2canvas !== 'undefined',
                        loadedMsg: 'html2canvas依赖已加载',
                        loadingMsg: '正在引入pdf所需html2canvas依赖',
                        errorMsg: 'html2canvas加载失败'
                    }
                ];

                // 加载单个脚本的函数，返回Promise
                const loadScript = (script) => {
                    return new Promise((resolve, reject) => {
                        // 检查是否已加载
                        if (script.check()) {
                            console.log(script.loadedMsg);
                            resolve();
                            return;
                        }

                        console.log(script.loadingMsg);

                        // 检查是否已有相同脚本正在加载
                        let scriptElement = document.getElementById(script.id);
                        if (scriptElement) {
                            // 如果已有该脚本，等待其加载完成
                            const checkLoaded = () => {
                                if (script.check()) {
                                    resolve();
                                } else {
                                    setTimeout(checkLoaded, 100);
                                }
                            };
                            checkLoaded();
                            return;
                        }

                        // 创建新脚本元素
                        scriptElement = document.createElement('script');
                        scriptElement.id = script.id;
                        scriptElement.src = script.src;
                        scriptElement.type = 'text/javascript';

                        // 设置超时
                        const timeout = setTimeout(() => {
                            reject(new Error(`${script.id}加载超时`));
                            scriptElement.remove();
                        }, 10000); // 10秒超时

                        // 加载成功处理
                        scriptElement.onload = () => {
                            clearTimeout(timeout);
                            console.log(script.loadedMsg);
                            resolve();
                        };

                        // 加载失败处理
                        scriptElement.onerror = () => {
                            clearTimeout(timeout);
                            console.error(script.errorMsg);
                            reject(new Error(script.errorMsg));
                            scriptElement.remove();
                        };

                        document.head.appendChild(scriptElement);
                    });
                };

                // 加载所有必要的脚本
                const loadAllScripts = async () => {
                    try {
                        // 并行加载所有需要的脚本
                        await Promise.all(scripts.map(script => loadScript(script)));
                        // 所有脚本加载完成，调用导出函数
                        exportToPDF();
                    } catch (error) {
                        console.error('脚本加载过程中发生错误:', error.message);
                        // 可以在这里添加错误处理逻辑，如提示用户
                    }
                };

                // 开始加载流程
                loadAllScripts();
            };

            // 绑定导出按钮事件
            exportBtn.addEventListener('click', checkLib);

            // 初始化时显示所有题目
            updateDisplayByExportType('all');
        };

        // 启动初始化流程
        init();
    }


}

// 初始化应用
(function () {
    'use strict';
    // 创建应用实例，启动工具
    new FenbiPaperTool();
})();
