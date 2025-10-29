# Utterances 评论系统配置指南

## 📋 什么是 Utterances？

Utterances 是一个基于 GitHub Issues 的轻量级评论系统，完全免费且无广告。

## 🚀 配置步骤

### 1. 安装 Utterances GitHub App

1. 访问: https://utteranc.es
2. 页面会显示配置选项
3. 选择你的仓库配置：
   - **repo**: `aiyolo/blog`
   - **Issue Term**: `pathname`（推荐）
   - **Issue Label**: `comment`（推荐）
   - **Theme**: `GitHub Light` / `GitHub Dark`

4. **点击 "Enable Utterances"**

### 2. 复制配置代码

utterances 会生成类似这样的代码：

```html
<script src="https://utteranc.es/client.js"
        repo="aiyolo/blog"
        issue-term="pathname"
        label="comment"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
```

### 3. 配置已完成

你的 Hugo 配置文件已经包含了正确的 utterances 配置：

```toml
[params.page.comment.utterances]
  enable = true
  repo = "aiyolo/blog"
  issueTerm = "pathname"
  label = "comment"
  theme = "github-light"
  themeDark = "github-dark"
```

## 🎯 完成后的效果

- ✅ 访客可以使用 GitHub 账号登录评论
- ✅ 每篇文章会自动创建对应的 GitHub Issue
- ✅ 支持完整的 Markdown 语法
- ✅ 支持表情符号和代码高亮
- ✅ 评论会同步到 GitHub Issues
- ✅ 完全免费且无广告
- ✅ 数据存储在你自己的 GitHub 仓库中

## 📱 测试评论功能

配置完成后，访问任意博客文章页面，在底部应该可以看到评论区。

## 🔧 主题切换

utterances 支持明暗主题切换：
- 浅色主题：`github-light`
- 深色主题：`github-dark`

你的博客已经配置了自动主题切换功能。

## 📄 查看评论

你可以直接在 GitHub 仓库中查看和管理评论：
- 访问: https://github.com/aiyolo/blog/issues
- 每个 Issue 对应一篇文章的评论

## 🔧 故障排除

如果评论区没有显示：
1. 确认 utterances GitHub App 已安装
2. 检查仓库是否为公开仓库
3. 检查浏览器控制台是否有错误信息
4. 确认文章的 front matter 中包含 `comments: true`