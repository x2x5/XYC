# 架构设计文档

## 技术栈

- HTML
- Tailwind CSS（编译为静态 CSS）
- GitHub Pages
- 可选：极小 JavaScript（仅用于手动主题切换）

## 目录结构

```
xiangyichu-shiyichu/
├── index.html
├── 404.html
├── README.md
├── docs/
│   ├── PRODUCT_REQUIREMENTS.md
│   ├── ARCHITECTURE.md
│   ├── CONTENT_GUIDE.md
│   ├── STYLE_GUIDE.md
│   ├── AI_WORKFLOW.md
│   ├── DEPLOYMENT.md
│   └── CHANGELOG.md
├── assets/
│   ├── css/
│   │   ├── input.css
│   │   └── main.css
│   ├── js/
│   └── images/
├── templates/
│   ├── home-card.html
│   ├── thought-index.html
│   └── thought-page.html
└── thoughts/
    └── {thought-slug}/
        ├── index.html
        └── {page-slug}.html
```

## 页面类型

| 类型 | 路径 | 说明 |
|------|------|------|
| 首页 | /index.html | 展示母题卡片 |
| 母题入口 | /thoughts/{slug}/index.html | 母题总入口 |
| 子页面 | /thoughts/{slug}/{page}.html | 具体想法页面 |
| 404 | /404.html | 自定义 404 |

## 路径规则

- 所有内部链接使用相对路径
- 不使用根路径 `/xxx`
- CSS 链接根据页面层级调整相对路径

## CSS 构建方式

```bash
npx @tailwindcss/cli -i ./assets/css/input.css -o ./assets/css/main.css --minify
```

## JavaScript 使用边界

- 第一版：完全无 JavaScript
- 增强版：仅允许极小 theme.js 用于手动主题切换
