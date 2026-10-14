---
layout: post
title: 用 Jekyll 搭一个不需要 Node.js 的博客
date: 2026-10-15
excerpt: 不装 Node.js、不装 npm、不引外部 CDN，只靠 Markdown 加 GitHub Actions，就能拥有一个能持续写作的个人博客。
tags:
  - Jekyll
  - GitHub Pages
  - 建站
---

我一直想有一个自己的地方写东西，但每次看到「先安装 Node.js、再 npm install、然后配置构建工具」就停下来了。

这次换了一条路：**不装任何前端工具链**。整个博客由纯 HTML、CSS 和 Markdown 组成，构建交给 GitHub 完成。

## 这套方案由四部分组成

| 部分 | 作用 |
| --- | --- |
| Markdown 文章 | 我只负责写内容，放在 `_posts/` 目录 |
| Jekyll 模板 | 把 Markdown 套进统一的页面骨架 |
| GitHub Actions | 每次推送后自动把 Markdown 编译成 HTML |
| GitHub Pages | 把编译结果发布成一个公开网址 |

关键点是：**编译发生在 GitHub 的服务器上，不在我的电脑上。** 所以本机不需要安装 Ruby、Jekyll、Node.js 或 npm。

## 写一篇新文章只需要三步

1. 在 `_posts/` 里新建一个文件，命名成 `YYYY-MM-DD-标题.md`
2. 顶部写上 Front Matter：

```yaml
---
layout: post
title: 文章标题
date: 2026-10-15
excerpt: 一句话摘要
tags:
  - 标签
---
```

3. 下面直接用 Markdown 写正文，然后 commit、push

推送之后我会在仓库的 Actions 页面看到构建进度，通常一两分钟就能在网站上读到新文章。

## 为什么不做「更高级」的方案

我特意没有引入 React、Vue、Vite 这类工具。原因是：

- 只是想写字，不需要复杂的状态管理和组件系统
- 依赖越少，几年后回来还能跑得起来
- 页面全部是静态 HTML，加载快，也不需要服务器
- 没有外部 CDN，页面不依赖任何第三方服务是否可用

> 工具应该服务于「我想持续写下去」这件事，而不是成为写下去的门槛。

## 接下来想做的事

- 把配色和排版再调得舒服一点
- 补上以前写的读书笔记
- 学会用分支来试验新样式，而不是直接改主分支

如果你也在犹豫要不要开始写博客，我的建议是：**先找一套只需要写 Markdown 的方案，把第一篇文章发出去。** 剩下的都可以慢慢来。
