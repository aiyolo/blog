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

## 行为准则

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

如果需要自定义主题行为，请使用以下方法：

1. **通过 Hugo 配置文件** - 在 `hugo.toml` 中修改主题参数
2. **创建本地布局覆盖** - 在 `layouts/` 目录创建文件覆盖主题布局
3. **添加自定义CSS/JS** - 在 `static/` 目录添加样式和脚本
4. **选择兼容的主题版本** - 使用与 Hugo 版本兼容的主题

### 📝 具体案例

**错误做法**：
```bash
# 禁止这样做
vim themes/FixIt/layouts/_markup/render-passthrough.html
```

**正确做法**：
```bash
# 推荐这样做
layouts/_markup/render-passthrough.html  # 创建本地覆盖
# 或者
hugo.toml  # 通过配置文件修改
```

## 下一步计划
1. 创建 GitHub 仓库 `aiyolo/my-blog`
2. 推送代码到 GitHub
3. 配置 GitHub Pages 自动部署
4. 安装 utterances GitHub App
5. 测试完整的博客功能