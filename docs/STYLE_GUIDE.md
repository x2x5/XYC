# 视觉与前端样式规范

## 总体风格

黑白灰为主，安静、文字优先、留白充足。像个人思想档案。

## 色彩

### 浅色模式
- 背景：`zinc-50` / `white`
- 正文：`zinc-950`
- 次级文字：`zinc-600`
- 边框：`zinc-200`

### 深色模式
- 背景：`zinc-950`
- 正文：`zinc-50`
- 次级文字：`zinc-400`
- 边框：`zinc-800`

## 字号

- 首页大标题：`text-4xl` / `sm:text-5xl`
- 页面标题：`text-4xl`
- 章节标题：`text-2xl`
- 正文：`text-base`
- 次级文字：`text-sm`

## 行高

- 正文：`leading-8`
- 正文（移动端基准）：`leading-7`

## 卡片样式

- 圆角：`rounded-3xl`
- 边框：`border border-zinc-200 dark:border-zinc-800`
- 背景：`bg-white dark:bg-zinc-950`
- 阴影：`shadow-sm`
- Hover：`hover:-translate-y-1 hover:shadow-md`

## 内容页样式

- 最大宽度：`max-w-3xl`
- 内边距：`px-6 py-12 sm:py-16`
- 链接：下划线 + `decoration-zinc-400`，hover 变深

## 深色模式规则

所有颜色必须同时提供浅色和深色版本，使用 `dark:` 变体。
