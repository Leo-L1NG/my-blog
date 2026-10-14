# Leo LING 的个人博客

基于 [nice-template](https://github.com/yejianqin61-cell/nice-template) 搭建，是一个不需要 Node.js、npm 或 React 的 Jekyll 静态博客。

- 仓库：https://github.com/Leo-L1NG/my-blog
- 网址：https://leo-l1ng.github.io/my-blog/

## 这份 README 与模板的区别

本仓库已经在模板基础上做了个人化修改：站点标题与描述、导航、页脚链接、首页文案与项目卡片、关于页、配色，以及 `_posts/` 中的文章。
以下步骤保留作为参考，前两步（创建仓库、启用 Pages）已经完成。

## 开箱步骤

1. 打开模板仓库，点击 **Use this template → Create a new repository**。
2. 填写自己决定的仓库名称和公开/私有可见性。
3. 创建完成后，进入自己仓库的 **Settings → Pages**，把 Source 设为 **GitHub Actions**。
4. 等待 `Build and deploy Jekyll site` workflow 完成，再打开 Pages URL。
5. 修改 `_config.yml` 中的名字，编辑 `index.html` 的项目卡片，并在 `_posts/` 中写自己的 Markdown 文章。

仓库创建和 Pages 设置也可以让 Agent 操作，但必须先把目标仓库 URL 明确告诉 Agent，并在推送前检查 `git diff`。

注意：仓库里的 `index.html` 是 Jekyll 模板源码，不能靠双击本地文件看到最终页面；最终 HTML 会由 GitHub Actions 生成。学生不需要在电脑上安装 Ruby、Jekyll、Node.js 或 npm。

## 关于文章日期（重要）

文章的**文件名日期**和 Front Matter 里的 date 必须是**今天或更早**。

GitHub Actions 运行在 **UTC 时区**。如果你在中国时间凌晨（UTC 前一天）提交一篇日期写着今天的文章，Jekyll 会认为它是**未来文章**并静默跳过——文章不会出现在首页，构建日志里只有一行：

```text
Skipping: _posts/xxx.md has a future date
```

**做法**：日期比本地日期早一天最保险。例如本地是 10 月 15 日凌晨，文件名和 date 就写 2026-10-14。

## 写一篇新文章

在 `_posts/` 中复制示例文章，文件名使用：

```text
YYYY-MM-DD-title.md
```

文章开头保留 Front Matter：

```yaml
---
layout: post
title: 文章标题
date: 2026-10-08
excerpt: 一句话摘要
tags:
  - 学习
---
```

第二个 `---` 之后直接写 Markdown 正文：标题、段落、列表、链接、代码块都可以使用。

## 发布流程

1. 修改或新增 `_posts/*.md`。
2. 修改首页内容时编辑 `index.html`。
3. 修改关于页时编辑 `about.md`。
4. 修改配色和排版时编辑 `assets/style.css`。
5. 在浏览器中检查文件内容和链接。
6. `git diff` 检查变更。
7. `git add`、`git commit`、`git push`。
8. GitHub Actions 自动运行 Jekyll，将 Markdown 编译成 HTML 并发布到 GitHub Pages。

## 第一次启用 Pages

把仓库推送到 GitHub 后，在仓库中打开：

```text
Settings → Pages → Source → GitHub Actions
```

之后每次推送到 `main`，workflow 都会重新生成网站。

## 需要学生理解的概念

```text
Markdown 文章
      ↓
Jekyll / GitHub Actions
      ↓
HTML 页面
      ↓
GitHub Pages URL
```

学生不需要在本地安装 Ruby、Jekyll、Node.js 或 npm。构建发生在 GitHub Actions 上。

## 这个仓库里各文件的作用

| 文件 | 改它的场合 |
| --- | --- |
| `_config.yml` | 改站点标题、描述、语言 |
| `index.html` | 改首页文案、头像首字母、项目卡片 |
| `_layouts/default.html` | 改导航栏、页脚（GitHub 链接、邮箱） |
| `_layouts/post.html` | 改文章页排版 |
| `about.md` | 改「关于我」页面 |
| `assets/style.css` | 改配色与排版（颜色集中在文件开头的 `:root` 变量里） |
| `_posts/*.md` | 新增和修改文章 |

## 本站遵守的约束

- 不引入 React、Vue、Node.js、npm、外部 CDN 或任何构建工具
- 只使用纯 HTML、CSS 和 Markdown
- 样式全部写在 `assets/style.css` 里，不依赖外部字体或脚本

## 提交与推送

改完文件后，在本仓库目录执行：

```bash
git add -A
git commit -m "说明这次改了什么"
git push
```

推送后 workflow 会自动重新构建，通常 1～2 分钟后网站更新。
