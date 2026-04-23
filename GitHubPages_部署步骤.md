# 部署到 GitHub Pages（稳定网址）

本项目是纯静态网站（`index.html` + 图片），最适合用 GitHub Pages 部署。

## 1) 在 GitHub 创建仓库

1. 打开 GitHub → New repository
2. Repository name 建议：`yz-ga4`（你可以自定义）
3. 选择 Public（老师一般要求公开 URL）
4. Create repository

## 2) 把本地项目推送到 GitHub

在本项目目录（包含 `index.html` 的文件夹）执行：

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<你的仓库名>.git
git push -u origin main
```

## 3) 启用 Pages（用 GitHub Actions 发布）

1. 进入你的仓库 → Settings → Pages
2. Build and deployment → Source 选择 GitHub Actions
3. 回到仓库首页 → Actions
4. 看到 “Deploy to GitHub Pages” 工作流成功后，Pages 会给你一个网址

## 4) 你的最终网址是什么？

通常是：

- `https://<你的用户名>.github.io/<你的仓库名>/`

例如仓库名是 `yz-ga4`，用户名是 `abc`，网址就是：

- `https://abc.github.io/yz-ga4/`

## 5) GA4 测试建议（用于 Realtime 截图）

用带调试参数的方式打开线上页面（便于确认事件已触发）：

- `https://<你的用户名>.github.io/<你的仓库名>/?debug=1`

然后做一次：选景点 → 点击“投我一票”，去 GA4 Realtime 截图即可。

