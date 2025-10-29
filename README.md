# 我的博客

一个基于 Hugo 和 FixIt 主题的个人博客，支持 GitHub 登录评论功能。

## 🚀 特性

- **🎨 现代化设计** - 使用 FixIt v0.4.0-alpha 主题
- **📱 响应式布局** - 完美适配移动端和桌面端
- **🔍 强大搜索** - 基于 Fuse.js 的全文搜索
- **💬 评论系统** - 支持 GitHub 账号登录 (giscus)
- **🌙 主题切换** - 支持深色/浅色主题
- **📝 Markdown 支持** - 完整的 Markdown 语法支持
- **🏷️ 分类标签** - 灵活的内容分类系统
- **⚡ 快速加载** - Hugo 的高速构建能力

## 🛠️ 技术栈

- **框架**: Hugo v0.151.2+
- **主题**: FixIt v0.4.0-alpha
- **评论**: giscus (基于 GitHub Discussions)
- **部署**: GitHub Pages

## 📂 项目结构

```
blog/
├── content/              # 博客内容
│   ├── posts/           # 博客文章
│   └── about.md         # 关于页面
├── themes/FixIt/        # FixIt 主题 (Git 子模块)
├── hugo.toml            # Hugo 配置文件
├── static/              # 静态资源
└── public/              # 生成的网站文件
```

## 🚀 快速开始

### 本地开发

```bash
# 克隆仓库
git clone https://github.com/aiyolo/blog.git
cd blog

# 启动开发服务器
hugo server --bind 0.0.0.0 --port 1313 --buildDrafts

# 访问网站
# http://localhost:1313
```

### 创建新文章

```bash
# 创建新文章
hugo new posts/my-new-post.md

# 编辑文章内容
# 确保文章的 front matter 中包含:
# comments: true
```

### 构建和部署

```bash
# 构建静态网站
hugo --minify

# 提交更改
git add .
git commit -m "更新博客内容"
git push origin main
```

## 📝 评论系统

本博客使用 [giscus](https://giscus.app/) 评论系统，支持：

- ✅ GitHub 账号登录
- ✅ Markdown 评论
- ✅ 表情符号支持
- ✅ 匿名评论
- ✅ 评论回复和点赞

## 🌐 在线访问

- **博客地址**: https://aiyolo.github.io/blog
- **GitHub 仓库**: https://github.com/aiyolo/blog

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来改进这个博客！

---

**使用 [FixIt](https://github.com/hugo-fixit/FixIt) 主题构建** 💙