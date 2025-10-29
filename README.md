# 我的博客

这是一个使用 [Hugo](https://gohugo.io/) 和 [PaperMod](https://github.com/adityatelange/hugo-PaperMod) 主题构建的个人博客。

## 🚀 快速开始

### 本地开发

1. 克隆仓库
   ```bash
   git clone --recursive https://github.com/yourusername/yourusername.github.io.git
   cd yourusername.github.io
   ```

2. 安装 Hugo
   ```bash
   # macOS
   brew install hugo

   # 其他平台请参考: https://gohugo.io/installation/
   ```

3. 启动本地服务器
   ```bash
   hugo server
   ```

   访问 http://localhost:1313 查看博客

### 创建新文章

```bash
hugo new content posts/my-new-post.md
```

### 部署

推送到 `main` 分支会自动触发 GitHub Actions 部署到 GitHub Pages。

## 📝 目录结构

```
my-blog/
├── content/           # 内容文件
│   ├── posts/        # 博客文章
│   └── about.md      # 关于页面
├── static/           # 静态资源
├── themes/           # 主题
├── .github/          # GitHub Actions
├── hugo.toml         # Hugo 配置文件
└── README.md         # 说明文件
```

## ⚙️ 配置

主要配置在 `hugo.toml` 文件中：

- `baseURL`: 你的 GitHub Pages 地址
- `title`: 博客标题
- `theme`: 使用主题
- `params`: 主题参数

## 🎨 主题自定义

当前使用 [PaperMod](https://github.com/adityatelange/hugo-PaperMod) 主题，支持：

- 🌙 暗黑/明亮模式切换
- 📱 响应式设计
- 🔍 搜索功能
- 📝 多种页面布局
- 🏷️ 标签和分类
- 📊 阅读时间统计

详细配置请参考 [PaperMod 文档](https://adityatelange.github.io/hugo-PaperMod/)

## 📝 写作指南

### Front Matter

每篇文章都需要包含 front matter：

```toml
+++
title = "文章标题"
date = 2025-10-25T23:00:00+08:00
description = "文章描述"
tags = ["标签1", "标签2"]
categories = ["分类"]
draft = false  # 设为 true 则不会发布
+++

文章内容...
```

### 推荐工具

- **写作**: Typora, VS Code
- **图片**: PicGo (图床上传)
- **语法检查**: markdownlint

## 🚀 部署到其他平台

### Netlify

1. 连接 GitHub 仓库
2. 构建命令: `hugo`
3. 发布目录: `public`

### Vercel

1. 导入项目
2. 框架预设: Other
3. 构建命令: `hugo`
4. 输出目录: `public`

## 📚 学习资源

- [Hugo 官方文档](https://gohugo.io/documentation/)
- [PaperMod 主题文档](https://adityatelange.github.io/hugo-PaperMod/)
- [Markdown 语法指南](https://www.markdownguide.org/basic-syntax/)

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

MIT License