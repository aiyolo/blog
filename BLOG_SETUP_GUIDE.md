# Hugo 博客完整配置指南

## 📋 项目概述

这是一个基于 Hugo 的个人博客项目，使用 FixIt 主题和 utterances 评论系统，部署在 GitHub Pages。

### 🎯 最终效果
- 🌐 **博客地址**: https://aiyolo.github.io/blog
- 🎨 **主题**: FixIt v0.4.0-alpha（现代化设计）
- 💬 **评论**: utterances（基于 GitHub Issues）
- 📱 **特性**: 响应式设计、搜索功能、分类标签、明暗主题切换

## 🚀 完整配置流程

### 第一阶段：项目初始化

#### 1. 创建 Hugo 项目
```bash
# 创建新项目
hugo new site my-blog

# 进入项目目录
cd my-blog

# 本地测试
hugo server --bind 0.0.0.0 --port 1313 --buildDrafts
```

#### 2. 添加 Git 版本控制
```bash
# 初始化 Git 仓库
git init
git add .
git commit -m "初始化 Hugo 博客项目"
```

### 第二阶段：主题选择和安装

#### 主题调研和选择过程：

1. **PaperMod**（初始选择）
   - ✅ 优点：简洁、功能完善、中文支持好
   - ❌ 问题：评论系统配置复杂，最终弃用

2. **Even**（尝试过）
   - ✅ 优点：设计优雅
   - ❌ 问题：配置要求复杂，最终弃用

3. **FixIt**（最终选择）
   - ✅ 优点：功能最丰富、现代化设计、完善的中文支持
   - ✅ 特性：搜索功能、PWA支持、多种评论系统支持

#### 安装 FixIt 主题：
```bash
# 添加为 Git 子模块
git submodule add https://github.com/hugo-fixit/FixIt.git themes/FixIt

# 更新配置文件 hugo.toml
theme = 'FixIt'
```

### 第三阶段：主题配置

#### FixIt 主题配置要点：

1. **作者信息必须是对象格式**（重要！）
```toml
# ❌ 错误格式
author = "aiyolo"

# ✅ 正确格式
[params.author]
  name = "aiyolo"
  email = "aiyolo@example.com"
  link = "https://github.com/aiyolo"
```

2. **基础配置**
```toml
baseURL = 'https://aiyolo.github.io/blog/'
languageCode = 'zh-cn'
title = '我的博客'
theme = 'FixIt'

[params]
  version = "0.3.X"
  title = "我的博客"
  description = "一个分享技术、生活和思考的博客"
  keywords = ["博客", "技术", "生活", "思考", "Hugo", "FixIt"]
```

3. **菜单配置**
```toml
[[menu.main]]
  identifier = "posts"
  name = "文章"
  url = "/posts/"
  weight = 1

[[menu.main]]
  identifier = "tags"
  name = "标签"
  url = "/tags/"
  weight = 2

[[menu.main]]
  identifier = "categories"
  name = "分类"
  url = "/categories/"
  weight = 3

[[menu.main]]
  identifier = "about"
  name = "关于"
  url = "/about/"
  weight = 4
```

### 第四阶段：评论系统配置

#### 评论系统选择过程：

1. **utterances**（第一选择）
   - ✅ 基础：基于 GitHub Issues
   - ✅ 优点：成熟稳定、完全免费、数据主权
   - ✅ 最终选择

2. **giscus**（尝试过）
   - ✅ 优点：基于 GitHub Discussions，功能更丰富
   - ❌ 问题：需要启用 Discussions，配置复杂

#### utterances 配置步骤：

1. **访问配置页面**: https://utteranc.es

2. **配置参数**:
   - **repo**: `aiyolo/blog`
   - **Issue Term**: `pathname`
   - **Issue Label**: `comment`
   - **Theme**: `GitHub Light`

3. **Hugo 配置**:
```toml
[params.page.comment]
  enable = true
  [params.page.comment.utterances]
    enable = true
    repo = "aiyolo/blog"
    issueTerm = "pathname"
    label = "comment"
    theme = "github-light"
    themeDark = "github-dark"
```

4. **安装 GitHub App**:
   - 在 utteranc.es 页面点击 "Enable Utterances"
   - 选择仓库 `aiyolo/blog`
   - 授权访问权限

### 第五阶段：GitHub Pages 部署

#### 部署挑战和解决方案：

1. **问题1**: GitHub Pages 默认使用 Jekyll，但项目是 Hugo
   - **解决方案**: 创建 `.nojekyll` 文件禁用 Jekyll

2. **问题2**: GitHub Actions 构建失败，版本不兼容
   - **错误信息**: `function "try" not defined`
   - **原因**: Hugo 版本与 FixIt 主题不兼容
   - **解决方案**: 使用兼容的 Hugo 版本 v0.147.7

3. **问题3**: 不能修改 submodule 文件
   - **重要约束**: 严禁修改 `themes/` 目录下的任何文件
   - **解决方案**: 创建本地布局覆盖 `layouts/_markup/render-passthrough.html`

#### 最终 GitHub Actions 工作流：

```yaml
name: Build and Deploy

on:
  push:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: "0.147.7"
          extended: true

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4

      - name: Build with Hugo
        run: hugo --minify --baseURL "${{ steps.pages.outputs.base_url }}"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

#### GitHub Pages 配置：

1. **仓库设置**: https://github.com/aiyolo/blog/settings/pages
2. **Source**: 选择 "GitHub Actions"
3. **自动部署**: 推送到 main 分支时自动触发

### 第六阶段：内容创建

#### 创建示例内容：

1. **关于页面** (`content/about.md`)
```markdown
---
title: "关于我"
date: 2025-10-25T23:00:00+08:00
draft: false
comments: true
---

## 你好！👋
[内容...]
```

2. **博客文章** (`content/posts/my-first-post.md`)
```markdown
---
author: "aiyolo"
title: "我的第一篇博客"
date: 2025-10-25T23:00:00+08:00
description: "欢迎来到我的博客！"
tags: ["博客", "介绍", "开始"]
categories: ["生活"]
draft: false
comments: true
---

[文章内容...]
```

## 🔧 重要配置文件

### `hugo.toml` (主要配置)
```toml
baseURL = 'https://aiyolo.github.io/blog/'
languageCode = 'zh-cn'
title = '我的博客'
theme = 'FixIt'

[params]
  version = "0.3.X"
  title = "我的博客"
  description = "一个分享技术、生活和思考的博客"
  
  [params.author]
    name = "aiyolo"
    email = "aiyolo@example.com"
    link = "https://github.com/aiyolo"

  # 评论系统
  [params.page.comment]
    enable = true
    [params.page.comment.utterances]
      enable = true
      repo = "aiyolo/blog"
      issueTerm = "pathname"
      label = "comment"
      theme = "github-light"
      themeDark = "github-dark"

# 菜单配置
[[menu.main]]
  identifier = "posts"
  name = "文章"
  url = "/posts/"
  weight = 1

# ... 其他配置
```

### `.nojekyll` (禁用 Jekyll)
```
# This file tells GitHub Pages to not use Jekyll
# Hugo will handle the site generation instead
```

### `layouts/_markup/render-passthrough.html` (本地布局覆盖)
```html
{{- /* 兼容版本的数学公式渲染模板 */ -}}
{{- /* 解决 Hugo 版本兼容性问题 */ -}}
[模板内容...]
```

## 🚨 行为准则和最佳实践

### 🔒 重要约束

**严禁修改任何 submodule 文件！**

- ❌ 绝对不能修改 `themes/` 目录下的任何主题文件
- ❌ 不能修改 submodule 中的模板、样式或配置文件
- ❌ 不能更改第三方主题的源代码

### ✅ 允许的操作

- ✅ 修改 Hugo 配置文件 (`hugo.toml`)
- ✅ 创建和编辑内容文件 (`content/` 目录)
- ✅ 修改本地布局文件 (`layouts/` 目录)
- ✅ 添加静态资源 (`static/` 目录)
- ✅ 通过配置文件自定义主题设置

### 🛠️ 主题配置方法

1. **通过 Hugo 配置文件** - 在 `hugo.toml` 中修改主题参数
2. **创建本地布局覆盖** - 在 `layouts/` 目录创建文件覆盖主题布局
3. **添加自定义CSS/JS** - 在 `static/` 目录添加样式和脚本
4. **选择兼容的主题版本** - 使用与 Hugo 版本兼容的主题

## 📱 使用指南

### 本地开发

```bash
# 启动开发服务器
hugo server --bind 0.0.0.0 --port 1313 --buildDrafts

# 访问 http://localhost:1313
```

### 创建新文章

```bash
# 创建新文章
hugo new posts/my-new-post.md

# 编辑文件，确保包含：
# comments: true
```

### 部署更新

```bash
# 提交更改
git add .
git commit -m "更新博客内容"
git push origin main

# GitHub Actions 会自动部署
```

## 🔧 故障排除

### 常见问题

1. **GitHub Pages 显示 "There isn't a GitHub Pages site here"**
   - 检查 GitHub Pages 设置是否选择 "GitHub Actions"
   - 等待 GitHub Actions 完成构建

2. **评论不显示**
   - 确认 utterances GitHub App 已安装
   - 检查文章 front matter 中是否有 `comments: true`
   - 检查浏览器控制台错误信息

3. **主题样式异常**
   - 确认 Hugo 版本与主题兼容
   - 检查是否误修改了 submodule 文件

4. **GitHub Actions 构建失败**
   - 检查工作流文件语法
   - 确认 Hugo 版本配置正确
   - 查看构建日志找出具体错误

## 📊 项目总结

### 技术栈
- **框架**: Hugo v0.147.7
- **主题**: FixIt v0.4.0-alpha
- **评论**: utterances (GitHub Issues)
- **部署**: GitHub Pages
- **CI/CD**: GitHub Actions

### 核心功能
- ✅ 响应式设计，移动端友好
- ✅ 深色/浅色主题切换
- ✅ 全文搜索功能
- ✅ 文章分类和标签
- ✅ GitHub 账号评论系统
- ✅ SEO 优化
- ✅ 快速加载性能

### 项目结构
```
blog/
├── content/              # 博客内容
│   ├── posts/           # 博客文章
│   └── about.md         # 关于页面
├── layouts/             # 本地布局覆盖
├── static/              # 静态资源
├── themes/FixIt/        # FixIt 主题 (Git 子模块)
├── .github/workflows/   # GitHub Actions 配置
├── hugo.toml            # Hugo 主配置
├── .nojekyll            # 禁用 Jekyll
└── README.md            # 项目说明
```

## 🎯 后续优化建议

1. **SEO 优化**: 添加更详细的 meta 信息
2. **内容丰富**: 定期发布高质量文章
3. **性能优化**: 压缩图片，使用 CDN
4. **功能扩展**: 添加 RSS 订阅、社交媒体分享
5. **备份策略**: 定期备份内容和配置

---

**项目创建时间**: 2025年10月29日  
**最终配置版本**: Hugo v0.147.7 + FixIt v0.4.0-alpha  
**部署平台**: GitHub Pages  
**评论系统**: utterances (基于 GitHub Issues)