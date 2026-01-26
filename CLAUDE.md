# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个基于 GitSite 静态网站生成器的个人学习文档网站项目。

## 技术栈

- **静态网站生成器**: GitSite (gitsite-cli)
- **主题**: GitSite 默认主题 + Tailwind CSS
- **前端**: HTML, CSS (Tailwind), JavaScript
- **构建系统**: Node.js CLI 工具
- **部署**: GitHub Pages
- **版本控制**: Git + 子模块

## 常用命令

### 环境准备
```bash
# 安装 GitSite CLI（全局）
npm install gitsite-cli -g
```

### 开发和构建
```bash
# 构建网站
gitsite-cli build -o _site -v

# 启动开发服务器
gitsite-cli serve -p 3010

```

### 导出 PDF

访问链接导出 AI-Coding
http://localhost:3000/Learning2Peak/books/AI-Coding/pdf

文件会自动生成并下载，首先保存到 .cache 目录，然后是浏览器下载目录。

[参考文档](https://gitsite.org/books/gitsite-guide/create-pdf/index.html)

## 项目结构

关键目录：
- `source/` - 所有内容和配置文件
  - `blogs/tech/` - 技术博客文章
  - `books/ClaudeCode/` - Claude Code 指南书籍
  - `pages/` - 静态页面
  - `static/` - 静态资源（CSS、JS、图片）
  - `site.yml` - 网站主配置文件
- `themes/default/` - GitSite 默认主题（Git 子模块）
- `.github/workflows/` - GitHub Actions 工作流

## 架构特点

1. **内容优先架构**：所有内容以 Markdown 文件存储在 `source/` 目录
2. **主题系统**：使用 GitSite 主题系统，默认主题为 Git 子模块
3. **配置驱动**：网站行为由 YAML 配置文件控制
4. **静态生成**：生成静态 HTML 文件，性能和安全性最佳
5. **Git 工作流**：内容版本控制和部署与 Git 工作流绑定

## 重要配置文件

- `source/site.yml` - 网站主配置（域名、导航、作者、分析等）
- `source/blogs/tech/blog.yml` - 博客配置
- `source/books/ClaudeCode/book.yml` - 书籍配置
- `themes/default/tailwind.config.js` - Tailwind CSS 配置

## 开发注意事项

- 修改内容时，确保所有 Markdown 文件格式正确
- GitSite uses Nunjucks as the template engine, rendering Markdown documents in real time for local preview, and converting markdown documents to HTML files in build mode.
- 自定义 JavaScript 请编辑 `source/static/custom.js`
- 新增内容需要在相应的配置文件中注册
- 确保在提交前本地构建测试通过

## 部署

项目使用 GitHub Actions 自动部署到 GitHub Pages：
- 推送到主分支会自动构建和部署
- PDF 生成工作流会自动创建书籍和博客的 PDF 版本
- 确保仓库设置正确配置了 GitHub Pages

## 特殊要求

- 需要 Node.js 20+
- Git 子模块必须初始化
- 如需使用自定义域名，请正确配置 DNS
- Google Analytics 和 Disqus 需要在配置中正确设置