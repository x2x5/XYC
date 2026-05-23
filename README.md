# 想一出是一出

一个由网页组成的个人思考迷宫。记录一个想法如何从一句直觉，逐步通过 AI 辅助调研、实验、反驳、补充，生长成更复杂的理解。

## 本地查看

直接打开 `index.html` 即可浏览。

## 生成 CSS

```bash
npx @tailwindcss/cli -i ./assets/css/input.css -o ./assets/css/main.css --minify
```

开发时可以加 `--watch` 自动监听：

```bash
npx @tailwindcss/cli -i ./assets/css/input.css -o ./assets/css/main.css --watch
```

## 新增一个想法页面

参考 `templates/` 目录下的模板：

- `templates/home-card.html` — 首页卡片
- `templates/thought-index.html` — 母题入口页
- `templates/thought-page.html` — 子页面

1. 如果是新母题，在 `thoughts/` 下创建目录和 `index.html`，然后在首页添加卡片
2. 如果是已有母题的新子页面，在对应目录下创建 `{slug}.html`，然后更新母题入口页的链接列表

所有内部链接使用相对路径。所有页面须支持深色模式。

## 部署

推送到 GitHub 仓库，启用 GitHub Pages（Source: Deploy from branch `main`, folder `/root`）。

详见 `docs/DEPLOYMENT.md`。
