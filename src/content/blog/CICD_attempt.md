---
title: "初步尝试搭建 CI/CD 流程"
description: "使用 GitHub Actions 为 Astro 博客搭建自动构建与部署流程。"
pubDatetime: 2026-09-08
tags:
  - CI/CD
  - GitHub Actions
  - Astro
draft: false
---

最近给博客简单搭了一套 CI/CD 流程。目标很直接：以后在本地写完文章，只需要 `git push`，服务器上的网站就能够自动更新，不再需要手动 SSH 到服务器执行部署。

## 整体流程

目前博客使用 Astro 构建，代码托管在 GitHub，网站则运行在 Azure VM 上，由 Caddy 提供静态文件服务。

整个流程如下：

```text
本地修改博客
    ↓
git push origin main
    ↓
GitHub Actions 自动触发
    ↓
安装 Node.js 与项目依赖
    ↓
执行 npm run build
    ↓
生成 dist/
    ↓
通过 SSH + rsync 上传
    ↓
Azure VM /srv/www/vm-blog/
    ↓
Caddy 提供最新的静态页面