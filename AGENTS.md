# 博客项目管理和配置

## 项目概述
这是一个基于 Hugo 的个人博客项目，使用 PaperMod 主题，配置了 utterances 评论系统，支持 GitHub 账号登录评论。

## 技术栈
- **框架**: Hugo v0.151.2+
- **主题**: PaperMod
- **评论系统**: utterances (基于 GitHub Issues)
- **部署**: GitHub Pages
- **版本控制**: Git

## 项目结构
```
blog/
├── AGENTS.md              # 项目管理文档
├── CLAUDE.md              # 软链接到 AGENTS.md
├── README.md              # 项目说明文档
├── hugo.toml              # Hugo 主配置文件
├── .gitignore             # Git 忽略文件
├── .gitmodules            # Git 子模块配置
├── archetypes/            # 内容模板
├── assets/                # 资源文件
├── content/               # 博客内容
│   ├── posts/             # 博客文章
│   └── about.md           # 关于页面
├── data/                  # 数据文件
├── i18n/                  # 国际化文件
├── layouts/               # 自定义布局模板
├── static/                # 静态资源
├── themes/                # 主题文件
│   └── PaperMod/          # PaperMod 主题 (Git 子模块)
└── public/                # 生成的静态网站文件
```

## 核心功能
- ✅ 响应式设计，支持移动端
- ✅ 深色/浅色主题切换
- ✅ 代码高亮和复制功能
- ✅ 文章分类和标签
- ✅ SEO 优化
- ✅ 评论系统 (utterances)
- ✅ 社交媒体分享
- ✅ 搜索功能

## 评论系统配置
使用 utterances 提供基于 GitHub 的评论功能：

```toml
[params.utterances]
repo = "aiyolo/my-blog"           # GitHub 仓库地址
issueTerm = "pathname"           # 基于文章路径创建 Issue
label = "comment"                # Issue 标签
theme = "github-light"           # 浅色主题
themeDark = "github-dark"        # 深色主题
```

## 使用指南

### 1. 本地开发
```bash
# 启动开发服务器
hugo server --bind 0.0.0.0 --port 1313 --buildDrafts

# 访问网站
# http://localhost:1313
```

### 2. 创建新文章
```bash
# 创建新文章
hugo new posts/my-new-post.md

# 编辑文章内容
# 在 content/posts/my-new-post.md 中添加内容
# 确保 front matter 中包含: comments = true
```

### 3. 部署到 GitHub Pages
```bash
# 构建静态文件
hugo --destination docs

# 提交更改
git add .
git commit -m "更新博客内容"
git push origin main
```

## 维护任务
- 定期更新 PaperMod 主题：`git submodule update --remote --merge`
- 备份内容到 GitHub 仓库
- 监控 utterances 评论状态
- 优化网站性能和 SEO

## 项目状态
- ✅ Hugo 框架配置完成
- ✅ PaperMod 主题安装完成
- ✅ utterances 评论系统配置完成
- ✅ 示例内容创建完成
- ⏳ GitHub 仓库创建和推送（待完成）
- ⏳ GitHub Pages 部署配置（待完成）

## 下一步计划
1. 创建 GitHub 仓库 `aiyolo/my-blog`
2. 推送代码到 GitHub
3. 配置 GitHub Pages 自动部署
4. 安装 utterances GitHub App
5. 测试完整的博客功能