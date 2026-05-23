# 《想一出是一出》静态超文本网站：项目需求文档与实现方案

版本：v1.0  
日期：2026-05-24  
定位：给后续执行 AI、网页生成 AI、以及未来的自己使用的完整规划文档。

---

## 0. 一句话定义

《想一出是一出》是一个部署在 GitHub Pages 上的纯静态个人思想网站。首页用卡片展示少数“母题 / 项目入口”，每个入口进入后不是传统博客列表，而是一组会不断生长、互相引用、互相跳转的 HTML 页面。整个网站像一个手工维护的超文本思想网络，记录一个想法如何从一句直觉，逐步通过 AI 辅助调研、实验、反驳、补充，生长成更复杂的理解。

---

## 1. 项目背景

### 1.1 创作动机

站长会不断产生一些不一定成熟、但很值得追踪的想法。例如：

> 问 AI 一个复杂问题时，如果让 AI 直接在网页聊天里回答，可能 2000 字左右就结束；但如果让 AI 输出一个可下载文件，它可能写出 5000 字甚至更完整的内容。那么“让 AI 生成文件”是否会带来更高质量、更充分、更有结构的回答？字数更多是否意味着模型投入了更多努力？

这个想法一开始可能只是一个直觉，但后续会继续生长：

- 先写一个原始问题页面。
- 再写一个调研页面。
- 再写一个反例页面。
- 再写一个实验设计页面。
- 再写一个结论修订页面。
- 每个页面里都可以超链接到其他页面。

因此，本网站不是“发表完成品”的地方，而是“记录想法如何变化”的地方。

### 1.2 网站气质

这个项目的核心气质是：

- 手工感。
- 静态。
- 可长期保存。
- 不依赖复杂框架。
- 不追求产品化。
- 不追求互动功能。
- 不追求社交传播。
- 重点是思想路径、跳转关系、页面之间的自然生长。

可以把它理解成：

- 不是传统博客。
- 不是作品集。
- 不是知识库系统。
- 不是 Notion 替代品。
- 不是 Wiki 系统。
- 而是一个“由网页组成的个人思考迷宫”。

---

## 2. 总体目标

### 2.1 产品目标

1. 建立一个极简、稳定、可长期维护的静态网站。
2. 首页以卡片形式展示主要项目 / 母题。
3. 每个项目点进去后，进入普通网页，不再强制卡片布局。
4. 普通网页之间通过 `<a>` 标签互相跳转，形成想法网络。
5. 所有页面都可以由 AI 根据站长想法生成。
6. 尽可能不使用 JavaScript。
7. 必须支持深色模式。
8. 必须适合 GitHub Pages 部署。
9. 必须让后续低智能执行 AI 也能按文档一步步实现。

### 2.2 技术目标

1. 使用 HTML 作为页面主体。
2. 使用 Tailwind CSS 作为样式系统。
3. 使用编译后的静态 CSS 文件，不在浏览器运行 Tailwind CDN。
4. 默认不使用前端框架，例如 React、Vue、Next.js。
5. 默认不使用数据库。
6. 默认不使用后端服务。
7. 默认不使用客户端运行时数据加载。
8. 所有跳转使用 HTML 原生 `<a href="...">`。
9. 页面在 GitHub Pages 上直接访问。
10. 页面即文件，文件即内容。

---

## 3. 核心原则

### 3.1 原则一：HTML 原生跳转，不需要 JavaScript

页面跳转只需要：

```html
<a href="../ai-output-quality/file-vs-chat.html">文件输出和网页回答的差异</a>
```

浏览器原生支持点击跳转。这个需求不需要 JavaScript。

### 3.2 原则二：首页是入口，不是全文索引

首页只展示主要项目 / 母题卡片。

错误理解：

> 每一篇页面都必须作为首页卡片展示。

正确理解：

> 首页只放“值得作为入口”的大想法。进入一个项目后，内部页面可以通过正文里的链接自然扩展。

### 3.3 原则三：页面网络优先于时间顺序

传统博客通常按日期排序。这个网站不以时间为第一组织方式，而以“想法之间的关系”为第一组织方式。

允许存在时间信息，但时间不是核心结构。

### 3.4 原则四：不用 001、002 作为主要命名

不建议把所有页面命名为 `001.html`、`002.html`，因为这个网站不是线性笔记。

推荐使用语义化英文 slug：

```text
ai-output-quality/
file-vs-chat.html
token-budget.html
experiment-design.html
```

也可以在页面标题里保留中文：

```html
<h1>让 AI 生成文件，回答质量会不会更高？</h1>
```

文件名负责稳定，标题负责表达。

### 3.5 原则五：AI 负责生成页面，人负责提出想法和判断方向

站长不需要亲自写大部分 HTML。站长提供：

- 想法原文。
- 想研究的问题。
- 希望页面表达的角度。
- 希望链接到哪些旧页面。

AI 负责：

- 生成页面结构。
- 生成 HTML。
- 使用既定样式。
- 添加标题、摘要、正文、链接、页脚。
- 保持站点一致性。

### 3.6 原则六：小米加步枪

本项目不追求“最现代”的技术栈，而追求：

- 够用。
- 稳定。
- 可读。
- 好修。
- 不容易坏。
- 未来十年仍然能打开。

---

## 4. 功能需求

## 4.1 首页卡片布局

首页文件：`index.html`

首页功能：

1. 展示网站名称：`想一出是一出`。
2. 展示一句简介。
3. 展示若干项目卡片。
4. 每个卡片是一个完整链接。
5. 卡片点击后进入对应项目入口页面。
6. 卡片支持 hover 效果。
7. 卡片在移动端单列，在桌面端多列。
8. 首页不需要动态加载。
9. 首页不需要搜索。
10. 首页不需要评论。

首页卡片字段建议：

- 项目标题。
- 一句话问题。
- 当前状态。
- 更新时间。
- 关键词标签。
- 入口链接。

示例卡片：

```html
<a href="./thoughts/ai-output-quality/" class="group block rounded-3xl border border-zinc-200 bg-white p-6 shadow-sm transition hover:-translate-y-1 hover:shadow-md dark:border-zinc-800 dark:bg-zinc-950">
  <p class="text-xs uppercase tracking-[0.24em] text-zinc-500">AI / 输出质量 / 实验</p>
  <h2 class="mt-4 text-2xl font-semibold text-zinc-950 dark:text-zinc-50">让 AI 生成文件，回答质量会更高吗？</h2>
  <p class="mt-3 text-sm leading-6 text-zinc-600 dark:text-zinc-400">一个关于输出载体、字数、努力程度和回答质量之间关系的想法。</p>
  <p class="mt-6 text-sm font-medium text-zinc-900 dark:text-zinc-100">进入这个想法 →</p>
</a>
```

---

## 4.2 项目入口页面

每个首页卡片点进去后，进入一个“项目入口页面”。

示例路径：

```text
/thoughts/ai-output-quality/index.html
```

项目入口页面不是卡片列表的复制，而是这个母题的“总入口”。它应该包含：

1. 项目标题。
2. 原始想法。
3. 当前理解。
4. 目前已经生长出来的页面链接。
5. 推荐阅读顺序。
6. 关键问题。
7. 反向返回首页的链接。

示例结构：

```html
<main>
  <a href="../../index.html">← 回到首页</a>

  <h1>让 AI 生成文件，回答质量会更高吗？</h1>

  <section>
    <h2>原始想法</h2>
    <p>我发现让 AI 直接回答时，它可能很快结束；但让它生成文件时，它可能写得更长、更完整。</p>
  </section>

  <section>
    <h2>已经生长出的页面</h2>
    <ul>
      <li><a href="./file-vs-chat.html">文件输出和网页回答到底有什么差异？</a></li>
      <li><a href="./length-vs-quality.html">字数更多是否等于质量更高？</a></li>
      <li><a href="./experiment-design.html">如何设计实验验证这个想法？</a></li>
    </ul>
  </section>
</main>
```

---

## 4.3 普通想法页面

普通页面是这个网站最重要的内容单位。

它们不需要卡片布局。它们就是正常网页。

一个普通想法页面应该包含：

1. 标题。
2. 元信息。
3. 本页核心问题。
4. 正文。
5. 页面内链接。
6. 相关页面。
7. 返回项目入口。
8. 返回首页。

推荐页面结构：

```html
<article class="mx-auto max-w-3xl px-6 py-16">
  <nav class="mb-10 text-sm">
    <a href="../../index.html">首页</a>
    <span>/</span>
    <a href="./index.html">AI 输出质量</a>
  </nav>

  <header>
    <p class="text-sm text-zinc-500">想法页面 / 2026-05-24 / 草稿</p>
    <h1>文件输出和网页回答到底有什么差异？</h1>
    <p>本页试图分析“让 AI 给我一个文件下载”是否真的会提升回答质量。</p>
  </header>

  <section>
    <h2>起点</h2>
    <p>……</p>
  </section>

  <section>
    <h2>进一步的问题</h2>
    <p>
      这个问题会自然连接到
      <a href="./length-vs-quality.html">字数更多是否等于质量更高</a>。
    </p>
  </section>

  <footer>
    <a href="./index.html">← 回到这个项目</a>
  </footer>
</article>
```

---

## 4.4 页面之间的超链接

链接是本网站的核心。

### 4.4.1 内部链接规则

优先使用相对路径。

同目录页面：

```html
<a href="./length-vs-quality.html">字数更多是否等于质量更高？</a>
```

返回上级项目：

```html
<a href="./index.html">回到项目入口</a>
```

返回首页：

```html
<a href="../../index.html">回到首页</a>
```

跨项目链接：

```html
<a href="../personal-knowledge-system/index.html">个人知识系统</a>
```

### 4.4.2 为什么不用根路径 `/xxx`

如果网站部署在 GitHub Pages 的项目站点，例如：

```text
https://username.github.io/xiangyichu-shiyichu/
```

那么 `/thoughts/...` 会指向：

```text
https://username.github.io/thoughts/...
```

这可能会错。

因此第一版统一用相对路径，降低部署风险。

### 4.4.3 外部链接规则

外部链接可以打开当前页，也可以加 `target="_blank"`。为了简单，默认不强制新窗口。

推荐写法：

```html
<a href="https://example.com" rel="noopener">外部资料</a>
```

如果使用新窗口：

```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">外部资料</a>
```

---

## 4.5 深色模式需求

深色模式是必需功能。

但是“深色模式”分两层：

### 4.5.1 第一层：自动深色模式，无 JavaScript

第一版必须支持根据用户系统偏好自动切换深色 / 浅色。

这可以纯 CSS 实现，不需要 JavaScript。

Tailwind 的 `dark:` 变体默认可以配合 `prefers-color-scheme` 使用。

示例：

```html
<body class="bg-zinc-50 text-zinc-950 dark:bg-zinc-950 dark:text-zinc-50">
```

如果用户系统是深色，页面自动深色。用户系统是浅色，页面自动浅色。

这符合“尽可能无 JS”的原则。

### 4.5.2 第二层：手动切换深色模式，需要决策

如果要求用户在网页里点击按钮，在“浅色 / 深色 / 跟随系统”之间切换，并且跨页面记住选择，那么通常需要极少量 JavaScript。

原因：

- HTML 可以跳转。
- CSS 可以响应系统主题。
- 但“记住用户选择”需要状态存储。
- 浏览器里最常见的状态存储是 `localStorage`。
- 操作 `localStorage` 需要 JavaScript。

因此本项目对深色模式做如下决策：

#### MVP 决策

第一版实现：

- 自动跟随系统深色模式。
- 不做手动切换按钮。
- 完全无客户端 JavaScript。

#### 增强版决策

如果站长明确要求“网页里必须有手动切换按钮”，则允许添加一个非常小的 `theme.js`，只做一件事：

- 切换并保存主题偏好。

这个 JavaScript 不负责页面内容、不负责路由、不负责动态加载、不负责复杂交互。

可以把它称为“主题开关例外”。

### 4.5.3 推荐的阶段策略

阶段一：先做自动深色模式。  
阶段二：如果真的觉得不够，再加入极小 JS 主题开关。  
阶段三：永远不要因为主题开关引入大型框架。

---

## 4.6 不需要的功能

第一版明确不做：

1. 评论系统。
2. 登录系统。
3. 后台管理系统。
4. 数据库。
5. 搜索。
6. 标签筛选。
7. 动态加载文章列表。
8. 无限滚动。
9. 点赞收藏。
10. 账号系统。
11. 复杂关系图谱。
12. SPA 单页应用路由。
13. React / Vue / Next.js。

---

## 5. “动态加载文章列表”是什么意思，以及为什么现在不需要

动态加载文章列表通常指：

1. 浏览器先打开一个空页面。
2. 页面里的 JavaScript 再去读取一个 JSON、API 或 Markdown 文件列表。
3. JavaScript 根据数据动态生成卡片。
4. 用户看到最终列表。

这个项目不需要这样做。

原因：

- 首页卡片数量不会一开始就非常大。
- 首页只放母题，不放所有页面。
- 手动维护 `index.html` 更直观。
- 静态 HTML 更稳定。
- 无 JavaScript 更符合实验精神。

未来如果首页卡片真的很多，可以引入“构建时生成”，而不是“运行时动态加载”。

构建时生成的意思是：

- 在本地或 GitHub Actions 里运行脚本。
- 脚本根据内容数据生成 `index.html`。
- 访问者打开的仍然是普通静态 HTML。
- 浏览器端仍然不需要 JavaScript。

这是未来可选升级，不是第一版需求。

---

## 6. 信息架构

## 6.1 推荐目录结构

```text
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
│   │   └── theme.js          # 可选；只有手动主题切换时才需要
│   └── images/
├── templates/
│   ├── home-card.html
│   ├── thought-index.html
│   └── thought-page.html
└── thoughts/
    ├── ai-output-quality/
    │   ├── index.html
    │   ├── file-vs-chat.html
    │   ├── length-vs-quality.html
    │   └── experiment-design.html
    └── another-thought/
        └── index.html
```

### 6.2 目录解释

#### `index.html`

网站首页。只放主要项目卡片。

#### `404.html`

自定义 404 页面。用于链接失效时显示友好提示。

#### `docs/`

项目文档目录。给人和 AI 看。

#### `assets/css/`

样式文件目录。

- `input.css`：Tailwind 输入文件。
- `main.css`：编译后的最终 CSS，页面实际引用它。

#### `assets/js/`

默认可以为空。只有在需要手动主题切换时才放 `theme.js`。

#### `templates/`

模板文件。AI 生成新页面时必须参考。

#### `thoughts/`

所有想法项目都放这里。

每一个母题一个目录。

---

## 7. 页面类型设计

## 7.1 首页 Home

路径：

```text
/index.html
```

职责：

- 解释网站是什么。
- 展示母题卡片。
- 让访问者进入某个思想分支。

不承担：

- 展示所有页面。
- 搜索全站。
- 展示最新动态流。

---

## 7.2 母题入口 Thought Index

路径：

```text
/thoughts/{thought-slug}/index.html
```

职责：

- 解释这个母题是什么。
- 展示它从哪里来。
- 汇总已经生长出的子页面。
- 提供建议阅读路径。

---

## 7.3 子页面 Thought Page

路径：

```text
/thoughts/{thought-slug}/{page-slug}.html
```

职责：

- 讨论一个具体问题。
- 从正文里自然链接到其他页面。
- 记录想法的一个局部变化。

---

## 7.4 辅助页面

可以有，但第一版不强制：

```text
/about.html       # 关于本站
/map.html         # 手工维护的站点地图
/links.html       # 外部资料
/changelog.html   # 网站更新记录，也可只用 docs/CHANGELOG.md
```

---

## 8. 内容模型

## 8.1 母题项目字段

每个母题建议记录：

```text
标题：让 AI 生成文件，回答质量会更高吗？
Slug：ai-output-quality
状态：草稿 / 生长中 / 暂停 / 阶段性结论
创建日期：2026-05-24
最后更新：2026-05-24
一句话问题：文件输出是否会诱导 AI 给出更长、更完整的回答？
关键词：AI、文件输出、回答质量、字数、实验
入口页面：thoughts/ai-output-quality/index.html
```

## 8.2 单页字段

每个普通页面建议记录：

```text
标题：字数更多是否等于质量更高？
Slug：length-vs-quality
所属母题：ai-output-quality
状态：草稿
创建日期：2026-05-24
最后更新：2026-05-24
本页问题：回答字数和回答质量之间是什么关系？
上一相关页：file-vs-chat.html
下一相关页：experiment-design.html
```

这些字段不一定要写成机器可读数据，可以直接写在 HTML 顶部。

---

## 9. 视觉设计方向

## 9.1 总体风格

关键词：

- 黑白灰为主。
- 安静。
- 文字优先。
- 卡片克制。
- 留白充足。
- 不花哨。
- 像个人思想档案，而不是商业产品。

## 9.2 首页视觉

首页可以更有设计感，因为它是入口。

建议：

- 大标题。
- 一段自我说明。
- 卡片网格。
- 卡片 hover 有轻微位移或阴影。
- 卡片内容不要太满。

## 9.3 内容页视觉

内容页应该像一篇可读性很高的文章。

建议：

- 最大宽度 `max-w-3xl` 或 `max-w-4xl`。
- 正文字号 `text-base` 或 `text-lg`。
- 行高 `leading-7` 或 `leading-8`。
- 标题层级清晰。
- 链接有下划线或明显颜色。
- 不要用过多边框和卡片。

## 9.4 深色模式视觉

浅色：

- 背景：`zinc-50` 或 `white`
- 正文：`zinc-900`
- 次级文字：`zinc-600`
- 边框：`zinc-200`

深色：

- 背景：`zinc-950`
- 正文：`zinc-50`
- 次级文字：`zinc-400`
- 边框：`zinc-800`

---

## 10. 技术实现方案

## 10.1 技术栈

```text
HTML
Tailwind CSS
GitHub Pages
可选：极小 JavaScript，仅用于手动主题切换
```

## 10.2 Tailwind 使用方式

推荐使用 Tailwind CLI 编译 CSS。

不要在最终网页里使用：

```html
<script src="https://cdn.tailwindcss.com"></script>
```

原因：

- 这会在浏览器运行 JavaScript。
- 不符合“尽可能不用 JS”的目标。
- 不适合作为正式生产方案。

推荐做法：

1. 写 `assets/css/input.css`。
2. 用 Tailwind CLI 生成 `assets/css/main.css`。
3. 所有 HTML 页面引用 `main.css`。

页面引用：

```html
<link rel="stylesheet" href="../../assets/css/main.css">
```

注意：不同目录层级要写对相对路径。

首页引用：

```html
<link rel="stylesheet" href="./assets/css/main.css">
```

子页面引用：

```html
<link rel="stylesheet" href="../../assets/css/main.css">
```

---

## 10.3 Tailwind 输入 CSS

`assets/css/input.css`：

```css
@import "tailwindcss";

@layer base {
  html {
    color-scheme: light dark;
  }

  body {
    @apply bg-zinc-50 text-zinc-950 antialiased dark:bg-zinc-950 dark:text-zinc-50;
  }

  a {
    @apply underline decoration-zinc-400 underline-offset-4 transition hover:decoration-zinc-900 dark:decoration-zinc-600 dark:hover:decoration-zinc-100;
  }
}
```

如果 Tailwind 版本或环境不支持某些写法，执行 AI 应参考当前 Tailwind 官方文档调整，但目标不变：输出一个静态 CSS 文件。

---

## 10.4 构建命令

推荐命令：

```bash
npx @tailwindcss/cli -i ./assets/css/input.css -o ./assets/css/main.css --watch
```

生产构建：

```bash
npx @tailwindcss/cli -i ./assets/css/input.css -o ./assets/css/main.css --minify
```

如果使用 Tailwind v3，命令可能略有不同；执行 AI 应以项目实际安装版本为准。

---

## 10.5 不用 JavaScript 时的主题策略

只使用系统主题：

```html
<body class="bg-zinc-50 text-zinc-950 dark:bg-zinc-950 dark:text-zinc-50">
```

这种方案：

- 无 JS。
- 简单。
- 稳定。
- 用户不能在网页里手动覆盖系统主题。

---

## 10.6 可选的极小主题切换 JS

只有在站长明确要求“网页里必须有按钮切换主题”时，加入以下文件。

`assets/js/theme.js`：

```js
(function () {
  const root = document.documentElement;
  const saved = localStorage.getItem('theme');
  const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;

  function applyTheme(theme) {
    if (theme === 'dark') {
      root.classList.add('dark');
    } else if (theme === 'light') {
      root.classList.remove('dark');
    } else {
      root.classList.toggle('dark', prefersDark);
    }
  }

  applyTheme(saved || 'system');

  window.setTheme = function (theme) {
    if (theme === 'system') {
      localStorage.removeItem('theme');
    } else {
      localStorage.setItem('theme', theme);
    }
    applyTheme(theme);
  };
})();
```

使用这个方案时，Tailwind 的 dark variant 要改成基于 `.dark` class，而不是只跟随系统。

这个方案属于“例外增强”，不改变网站的纯静态本质，因为：

- 服务器仍然是静态文件。
- 路由仍然是 HTML 链接。
- 内容不是 JS 生成的。
- JS 只负责主题偏好。

---

## 11. 模板规范

## 11.1 所有页面必须包含的基础结构

```html
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>页面标题 - 想一出是一出</title>
  <meta name="description" content="页面描述">
  <link rel="stylesheet" href="相对路径/assets/css/main.css">
</head>
<body>
  页面内容
</body>
</html>
```

## 11.2 内容页模板

```html
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>页面标题 - 想一出是一出</title>
  <meta name="description" content="本页摘要。">
  <link rel="stylesheet" href="../../assets/css/main.css">
</head>
<body class="bg-zinc-50 text-zinc-950 dark:bg-zinc-950 dark:text-zinc-50">
  <main class="mx-auto max-w-3xl px-6 py-12 sm:py-16">
    <nav class="mb-10 flex flex-wrap gap-2 text-sm text-zinc-500 dark:text-zinc-400">
      <a href="../../index.html">首页</a>
      <span>/</span>
      <a href="./index.html">所属母题</a>
    </nav>

    <article>
      <header class="mb-10">
        <p class="text-sm text-zinc-500 dark:text-zinc-400">草稿 / 2026-05-24</p>
        <h1 class="mt-3 text-4xl font-semibold tracking-tight text-zinc-950 dark:text-zinc-50">页面标题</h1>
        <p class="mt-5 text-lg leading-8 text-zinc-600 dark:text-zinc-400">页面导语。</p>
      </header>

      <div class="space-y-8 text-base leading-8 text-zinc-800 dark:text-zinc-200">
        <section>
          <h2 class="text-2xl font-semibold text-zinc-950 dark:text-zinc-50">小标题</h2>
          <p class="mt-4">正文。</p>
        </section>
      </div>
    </article>

    <footer class="mt-16 border-t border-zinc-200 pt-8 text-sm text-zinc-500 dark:border-zinc-800 dark:text-zinc-400">
      <p><a href="./index.html">← 回到所属母题</a></p>
    </footer>
  </main>
</body>
</html>
```

---

## 12. 项目内文档安排

这个项目本身应该包含以下文档。执行 AI 必须创建或维护它们。

## 12.1 `README.md`

给任何打开仓库的人看的入口说明。

应包含：

- 项目是什么。
- 如何本地查看。
- 如何生成 CSS。
- 如何新增一个想法页面。
- 如何部署。

## 12.2 `docs/PRODUCT_REQUIREMENTS.md`

产品需求文档。

应包含：

- 项目目标。
- 用户需求。
- 功能范围。
- 不做什么。
- 验收标准。

本文件可以由当前文档拆分得到。

## 12.3 `docs/ARCHITECTURE.md`

架构设计文档。

应包含：

- 技术栈。
- 目录结构。
- 页面类型。
- 路径规则。
- CSS 构建方式。
- JavaScript 使用边界。

## 12.4 `docs/CONTENT_GUIDE.md`

内容写作规范。

应包含：

- 什么是母题。
- 什么是子页面。
- 如何命名页面。
- 如何写原始想法。
- 如何写更新记录。
- 如何添加内部链接。

## 12.5 `docs/STYLE_GUIDE.md`

视觉与前端样式规范。

应包含：

- 色彩。
- 字号。
- 行高。
- 卡片样式。
- 内容页样式。
- 深色模式规则。

## 12.6 `docs/AI_WORKFLOW.md`

AI 协作流程文档。

应包含：

- 站长如何把想法交给 AI。
- AI 如何判断新建母题还是新建子页面。
- AI 如何生成 HTML。
- AI 如何维护链接。
- AI 输出前检查什么。

## 12.7 `docs/DEPLOYMENT.md`

部署文档。

应包含：

- GitHub Pages 设置。
- 本地构建 CSS。
- 提交流程。
- 常见路径错误。
- 如何修 404。

## 12.8 `docs/CHANGELOG.md`

变更记录。

应包含：

- 每次新增了哪些页面。
- 修改了哪些页面。
- 是否新增母题。
- 是否修改样式或结构。

---

## 13. AI 协作流程

## 13.1 判断：新建母题还是新建子页面

当站长提出一个新想法时，AI 先判断：

### 新建母题的条件

满足以下任意条件，可新建母题：

- 这个想法足够大，可以长期展开。
- 它会衍生多个问题。
- 它和已有母题关系不强。
- 它适合作为首页卡片入口。

### 新建子页面的条件

满足以下任意条件，应放入已有母题：

- 它是某个旧想法的延伸。
- 它是在回答旧页面里的一个问题。
- 它是某个母题下的实验、反驳、补充、资料整理。

## 13.2 新建母题流程

1. 创建目录：`thoughts/{slug}/`。
2. 创建入口页：`thoughts/{slug}/index.html`。
3. 在首页 `index.html` 添加卡片。
4. 在入口页写原始想法。
5. 预留“已经生长出的页面”区域。
6. 如果已有第一个子问题，同时创建第一个子页面。

## 13.3 新建子页面流程

1. 确定所属母题。
2. 创建 `{page-slug}.html`。
3. 页面顶部加面包屑导航。
4. 正文中加入相关内部链接。
5. 页面底部加入“回到母题入口”。
6. 回到母题入口页，添加该子页面链接。
7. 如有必要，在相关旧页面里添加反向链接。

## 13.4 页面更新流程

当某个旧想法被修正时，不一定要覆盖原文。

推荐做法：

- 保留旧想法。
- 新增“后来修正”段落。
- 链接到新页面。
- 在新页面说明为什么观点发生变化。

这个网站的价值正是“看见想法如何变化”。

---

## 14. 示例母题：AI 文件输出质量

## 14.1 母题目录

```text
thoughts/ai-output-quality/
├── index.html
├── file-vs-chat.html
├── length-vs-quality.html
├── effort-vs-output.html
└── experiment-design.html
```

## 14.2 母题入口标题

```text
让 AI 生成文件，回答质量会更高吗？
```

## 14.3 子页面规划

### `file-vs-chat.html`

问题：

> 文件输出和网页聊天回答到底有什么差异？

讨论方向：

- 输出格式是否影响组织结构。
- 文件是否让 AI 更像在完成正式交付物。
- 网页聊天回答是否更容易被压缩。

### `length-vs-quality.html`

问题：

> 字数更多是否等于质量更高？

讨论方向：

- 字数是质量指标之一，但不是充分条件。
- 长回答可能更全面，也可能只是重复。
- 质量还要看结构、准确性、论证、可操作性。

### `effort-vs-output.html`

问题：

> 输出更长是否意味着 AI 更努力？

讨论方向：

- “努力”是拟人化说法。
- 更长输出可能意味着提示词触发了更完整的任务模式。
- 需要区分模型能力、上下文预算、产品限制、输出格式。

### `experiment-design.html`

问题：

> 如何设计一个实验验证这个想法？

讨论方向：

- 同一个问题分别要求网页回答和文件输出。
- 比较字数、结构、引用、覆盖面、错误率、可执行性。
- 多轮重复实验，减少偶然性。

---

## 15. 验收标准

## 15.1 MVP 验收标准

第一版完成时，必须满足：

1. GitHub Pages 可以成功打开首页。
2. 首页有网站标题和简介。
3. 首页至少有 1 个母题卡片。
4. 点击卡片能进入母题入口页。
5. 母题入口页能链接到至少 1 个子页面。
6. 子页面能返回母题入口页。
7. 所有页面都能返回首页。
8. 页面跳转不依赖 JavaScript。
9. 页面在手机和桌面都能阅读。
10. 页面支持自动深色模式。
11. CSS 是编译后的静态文件。
12. 不使用数据库。
13. 不使用评论系统。
14. 不使用前端框架。
15. 仓库里有 README 和 docs 文档。

## 15.2 链接验收标准

1. 没有明显 404。
2. 所有内部链接使用相对路径。
3. 子页面的 CSS 路径正确。
4. 从任意页面至少能通过链接回到首页。
5. 从任意子页面至少能回到所属母题入口。

## 15.3 视觉验收标准

1. 首页卡片有清晰层级。
2. 内容页阅读舒适。
3. 深色模式下文字对比度足够。
4. 链接在浅色和深色下都可辨认。
5. 移动端没有横向滚动。

---

## 16. 未来可选升级

这些不是第一版需求。

## 16.1 搜索

如果页面很多，可以考虑：

- 静态搜索索引。
- Pagefind。
- Fuse.js。

但这会引入 JavaScript。只有当内容规模真的需要搜索时再做。

## 16.2 标签页

可以创建一个手工维护的：

```text
/tags.html
```

但不做动态筛选。

## 16.3 站点地图

可以创建：

```text
/map.html
```

用普通 HTML 列出所有母题和页面。

## 16.4 自动生成首页

未来可以用 Node、Python 或其他脚本从内容元数据生成首页。

注意：这是构建时自动化，不是浏览器运行时动态加载。

## 16.5 手动主题切换

如果系统主题不够用，再加入极小 `theme.js`。

## 16.6 关系图谱

如果未来页面关系非常复杂，可以生成一张静态 SVG 图，或者用 JS 画交互图。

第一版不做。

---

## 17. 风险与取舍

## 17.1 不使用 JavaScript 的风险

缺点：

- 无法方便做搜索。
- 无法方便做筛选。
- 无法方便做持久化主题按钮。
- 无法动态生成列表。

收益：

- 页面更稳。
- 更容易部署。
- 更容易维护。
- 更不容易被构建系统绑架。
- 更符合“静态思想网站”的实验精神。

结论：

第一版坚持无 JS 是合理的。

## 17.2 手写 HTML 的风险

缺点：

- 多页面会重复 header、footer、样式路径。
- 页面多了之后维护成本上升。

应对：

- 用模板文件降低重复劳动。
- 让 AI 按模板生成页面。
- 暂时接受手工维护。
- 未来再考虑构建工具。

## 17.3 使用 Tailwind 的风险

缺点：

- HTML class 会比较长。
- 如果不用组件化，重复 class 会多。

收益：

- 不用写大量自定义 CSS。
- AI 很擅长生成 Tailwind HTML。
- 响应式和深色模式方便。

结论：

Tailwind 适合本项目。

---

## 18. 给执行 AI 的开发任务清单

执行 AI 应按顺序完成：

1. 创建项目目录结构。
2. 创建 `README.md`。
3. 创建 `docs/` 下所有文档。
4. 配置 Tailwind CLI。
5. 创建 `assets/css/input.css`。
6. 编译生成 `assets/css/main.css`。
7. 创建 `index.html`。
8. 创建第一个母题目录：`thoughts/ai-output-quality/`。
9. 创建母题入口页：`thoughts/ai-output-quality/index.html`。
10. 创建第一个子页面：`file-vs-chat.html`。
11. 创建第二个子页面：`length-vs-quality.html`。
12. 创建第三个子页面：`experiment-design.html`。
13. 确保首页卡片能进入母题入口。
14. 确保母题入口能进入所有子页面。
15. 确保子页面能返回母题入口和首页。
16. 创建 `404.html`。
17. 检查移动端布局。
18. 检查深色模式。
19. 检查所有链接路径。
20. 提供部署说明。

---

## 19. 给执行 AI 的页面生成提示词模板

当站长给出新想法时，可以把以下提示词交给执行 AI。

```text
你正在维护一个叫《想一出是一出》的 GitHub Pages 静态网站。

这个网站的原则：
- 使用纯 HTML + Tailwind CSS。
- 默认不使用 JavaScript。
- 页面跳转只使用 <a> 标签。
- 首页只放母题卡片。
- 子页面是普通文章网页，通过正文链接自然生长。
- 所有内部链接使用相对路径。
- 所有页面必须支持深色模式。
- 不使用 React、Vue、Next.js、数据库、评论系统。

请根据以下想法，判断它应该成为：
1. 一个新的母题；还是
2. 某个已有母题下的新子页面。

然后按项目模板生成对应 HTML 文件，并告诉我需要修改哪些旧页面来添加链接。

我的新想法是：
【在这里粘贴想法】

已有母题包括：
【在这里列出已有母题】
```

---

## 20. 给执行 AI 的输出检查清单

每次生成或修改页面前，执行 AI 必须自查：

1. 是否使用了完整 HTML 文档结构？
2. `lang="zh-CN"` 是否存在？
3. `meta viewport` 是否存在？
4. CSS 路径是否按当前页面层级写对？
5. 所有内部链接是否为相对路径？
6. 是否误用了根路径 `/xxx`？
7. 是否误用了 JavaScript？
8. 是否支持 `dark:` 深色样式？
9. 是否有返回首页链接？
10. 是否有返回母题入口链接？
11. 页面标题是否清晰？
12. 页面是否保留原始想法，而不是过度包装？
13. 是否新增了必要的反向链接？
14. 是否更新了母题入口页？
15. 首页是否只在新母题时更新？

---

## 21. 部署方案

## 21.1 GitHub Pages 部署方式

推荐使用 GitHub Pages。

两种方式：

### 用户站点

仓库名：

```text
username.github.io
```

访问地址：

```text
https://username.github.io/
```

### 项目站点

仓库名：

```text
xiangyichu-shiyichu
```

访问地址：

```text
https://username.github.io/xiangyichu-shiyichu/
```

第一版为了路径稳定，建议所有内部链接都使用相对路径。

## 21.2 提交流程

```bash
git add .
git commit -m "Add initial static thought site"
git push
```

GitHub Pages 设置：

- Source：Deploy from a branch。
- Branch：`main`。
- Folder：`/root`。

如果未来使用 GitHub Actions，再单独升级部署方案。

---

## 22. 第一版最终形态

第一版完成后，访问者会看到：

1. 一个安静的首页。
2. 首页上有一个或几个大想法卡片。
3. 点进卡片后，进入某个想法的入口页面。
4. 入口页面解释这个想法从哪里来。
5. 页面里列出几个已经生长出来的分支。
6. 点进分支后，是正常文章页面。
7. 文章中继续链接到其他文章。
8. 整个网站像一个不断扩张的思想网络。
9. 没有登录、评论、复杂交互。
10. 深色模式可用。
11. GitHub Pages 可部署。
12. 后续页面可以持续由 AI 生成。

---

## 23. 最终决策摘要

| 问题 | 决策 |
|---|---|
| 点击跳转是否需要 JS | 不需要，HTML `<a>` 即可 |
| 首页是否动态加载卡片 | 不需要，手写静态 HTML |
| 是否每个页面都是卡片 | 不是，只有首页是卡片入口 |
| 页面命名是否用 001/002 | 不推荐，使用语义化 slug |
| 是否使用 Tailwind | 使用，但编译为静态 CSS |
| 是否使用 Tailwind CDN | 不使用 |
| 是否使用 React/Vue | 不使用 |
| 是否使用数据库 | 不使用 |
| 是否需要评论系统 | 不需要 |
| 是否支持深色模式 | 必须支持 |
| 深色模式第一版怎么做 | 跟随系统，无 JS |
| 手动深色切换怎么办 | 可选极小 JS 例外 |
| 后续内容谁写 | 由 AI 根据站长想法生成 |
| 本站核心价值 | 记录想法如何生长和分叉 |

---

## 24. 参考资料

- GitHub Pages 官方站点：https://pages.github.com/
- Tailwind CSS CLI 文档：https://tailwindcss.com/docs/installation/tailwind-cli
- Tailwind CSS Dark Mode 文档：https://tailwindcss.com/docs/dark-mode

