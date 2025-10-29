# Giscus 评论系统配置指南

## 📋 什么是 Giscus？

Giscus 是一个基于 GitHub Discussions 的评论系统，完全免费且无广告。

## 🚀 配置步骤

### 1. 安装 Giscus GitHub App

1. 访问: https://github.com/apps/giscus
2. 点击 "Install" 安装应用
3. 选择你的仓库 `aiyolo/blog`
4. 确认安装权限

### 2. 获取仓库信息

1. 访问: https://github.com/aiyolo/blog/discussions
2. 如果提示启用 Discussions，点击启用
3. 创建一个新的 "Announcements" 分类（如果还没有）

### 3. 配置 Giscus

1. 访问: https://giscus.app
2. 输入仓库信息：
   - **仓库**: `aiyolo/blog`
   - **页面 ↔️ discussions 映射关系**: `pathname`
   - **Discussion 分类**: `Announcements`
3. 复制生成的配置信息

### 4. 更新 Hugo 配置

将获取的配置信息更新到 `hugo.toml` 文件中：

```toml
[params.page.comment.giscus]
  enable = true
  repo = "aiyolo/blog"
  repoId = "R_kgDO..."  # 替换为实际的仓库 ID
  category = "Announcements"
  categoryId = "DIC_kwDO..."  # 替换为实际的分类 ID
  mapping = "pathname"
  strict = "0"
  reactionsEnabled = "1"
  emitMetadata = "0"
  inputPosition = "bottom"
  lang = "zh-CN"
  loading = "lazy"
```

## 🎯 完成后的效果

- ✅ 访客可以使用 GitHub 账号登录评论
- ✅ 支持 Markdown 和表情符号
- ✅ 评论会同步到 GitHub Discussions
- ✅ 可以点赞和回复评论
- ✅ 完全免费且无广告

## 📱 测试评论功能

配置完成后，访问任意博客文章页面，在底部应该可以看到评论区。

## 🔧 故障排除

如果评论区没有显示：
1. 检查 Giscus GitHub App 是否已安装
2. 确认仓库 ID 和分类 ID 是否正确
3. 检查浏览器控制台是否有错误信息
4. 确认文章的 front matter 中包含 `comments: true`