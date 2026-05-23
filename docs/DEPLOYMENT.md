# 部署文档

## GitHub Pages 设置

### 项目站点

仓库名：`xiangyichu-shiyichu`

访问地址：`https://username.github.io/xiangyichu-shiyichu/`

### 配置步骤

1. 在 GitHub 仓库页面进入 Settings → Pages
2. Source：Deploy from a branch
3. Branch：`main`
4. Folder：`/root`
5. Save

## 本地构建 CSS

```bash
npx @tailwindcss/cli -i ./assets/css/input.css -o ./assets/css/main.css --minify
```

## 提交流程

```bash
git add .
git commit -m "Add initial static thought site"
git push
```

## 常见路径错误

- 不要使用根路径 `/xxx` — 在项目站点下会指向错误 URL
- 始终使用相对路径：`../../index.html`
- 子页面的 CSS 路径应为 `../../assets/css/main.css`

## 如何修 404

- 检查文件是否存在
- 检查链接路径是否正确（相对路径层级）
- 检查文件名大小写
