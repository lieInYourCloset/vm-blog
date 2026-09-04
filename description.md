# Personal Blog — Design & Implementation Spec

## 1. 项目目标

构建一个轻量、现代、极简的个人博客。

技术方向：

- Astro
- 参考 AstroPaper 的项目结构与功能设计
- 视觉语言参考 https://coink.wang/
- 最终输出纯静态 HTML / CSS / JS
- 部署目标为 1 GB RAM 的 Azure Linux VM
- 使用 Caddy 提供静态文件服务
- 源码使用 Git 管理，并托管在 GitHub

核心原则：

> 一眼看起来很简单，但字体、间距、字号、标题、代码块、暗色模式等细节经过认真设计。

不要做成 Fuwari / Stack 那种明显的卡片式博客。


## 2. 视觉风格

整体采用 Typography-first 的极简设计。

关键词：

- Minimal
- Clean
- Typography-first
- Large whitespace
- Content-focused
- Quiet
- Modern

避免：

- 大量卡片
- 文章卡片阴影
- 多栏 Dashboard 式布局
- 复杂侧边栏
- 花哨渐变
- 大量圆角容器
- 大量动画
- 复杂 Hero Banner
- 过度装饰
- “模板感”很强的博客首页

页面应该让文章标题和文字本身成为主要视觉元素。


## 3. 首页

首页保持非常简单。

建议结构：

    Site Name
    一句简短的个人描述

    About   Projects   Archive

    2026

    文章标题                         Sep 04
    一两句话的文章摘要。
    tech / linux

    第二篇文章                       Aug 28
    一两句话的文章摘要。
    life

    2025

    ...

文章按照年份分组，并按发布时间倒序排列。

不要使用文章卡片。

标题、日期、摘要、Tag 应通过：

- 字号
- 字重
- 灰度
- 间距

建立视觉层级，而不是通过边框和容器建立层级。


## 4. Header

Header 极简。

桌面端大致：

    Blog Name                     About  Projects  Archive  ◐

其中：

- 左侧为站点名称
- 右侧为少量导航
- ◐ 为 Light / Dark Mode 切换

不要：

- 大型导航栏
- 彩色背景
- 汉堡菜单（桌面端）
- Logo 动画

移动端可以适当简化。


## 5. 文章页面

文章页是整个网站最重要的页面。

结构：

    Article Title

    2026-09-04 · tech · linux

    正文正文正文……

正文区域不要过宽。

建议正文最大宽度约：

    680px ~ 760px

重点优化：

- 中文阅读体验
- 英文阅读体验
- 中英文混排
- 行高
- 段落间距
- Heading 层级
- List
- Blockquote
- Inline Code
- Code Block
- Link
- Image
- Table


## 6. Typography

Typography 是整个设计的核心。

不要依赖大量 UI 元素制造“设计感”。

正文应：

- 字号舒适
- 行距略宽
- 段落间有明显但克制的间距
- 标题层级明确
- 字体颜色不要使用纯黑
- Dark Mode 不使用纯白正文

中文和英文混排时保持自然。

代码使用独立的等宽字体。


## 7. Code Block

技术博客会包含较多代码，因此代码块需要重点设计。

要求：

- 支持 Syntax Highlighting
- Light / Dark Mode
- 横向滚动
- 合理 padding
- 圆角非常轻微或没有圆角
- 与正文视觉上区分，但不要过度突出
- 支持 Copy Code 按钮

Inline code 也需要单独设计。

整体风格仍然保持克制。


## 8. Dark Mode

必须支持：

- Light
- Dark
- 跟随系统偏好
- 用户手动切换

Dark Mode 不要简单地：

    black + white

而应该使用稍柔和的深色背景和浅灰正文。

Light Mode 同样避免：

    #000 on #fff

尽量降低长时间阅读的视觉疲劳。


## 9. Archive

提供独立 Archive 页面。

结构保持简单：

    Archive

    2026
    Sep 04    Building My Blog
    Aug 20    Wi-Fi Sensing Notes
    ...

    2025
    ...

不要使用 Timeline UI。

使用普通排版即可。


## 10. Tags

支持 Tags。

例如：

    Linux
    Wi-Fi
    Sensing
    Programming
    Life
    Notes

点击 Tag 后：

    # Linux

    Article A
    Article B
    Article C

仍然使用简单文章列表，不使用卡片。


## 11. About

About 页面保持文章式排版。

可以包含：

- 简短介绍
- 技术兴趣
- 当前研究/项目
- GitHub
- Email

不要设计成复杂 Resume 页面。


## 12. Projects

Projects 可以比 Blog 稍微丰富一些，但仍然保持极简。

例如：

    Projects

    Wi-Fi Sensing
    Human presence detection using Wi-Fi CSI.
    GitHub →

    Linux Server
    Personal Linux / Docker experiments.
    GitHub →

允许 Projects 使用非常轻微的分隔线，但尽量不要使用大型 Card。


## 13. Blog Content

文章使用 Markdown / MDX 管理。

建议：

    src/content/blog/

每篇文章包含 Frontmatter：

    title
    description
    pubDatetime
    tags
    draft

例如：

    ---
    title: "Building My Personal Blog"
    description: "Some notes about building this site."
    pubDatetime: 2026-09-04
    tags:
      - linux
      - web
    draft: false
    ---


## 14. 功能要求

第一版至少实现：

- Markdown / MDX
- 首页文章列表
- 按年份分组
- Article 页面
- Archive
- Tags
- About
- Projects
- Dark Mode
- Responsive Design
- Syntax Highlighting
- RSS
- Sitemap
- SEO metadata

可以实现：

- Search
- Reading Time
- Copy Code

暂时不要实现：

- 评论系统
- 用户系统
- 数据库
- 后台 CMS
- 点赞
- 复杂统计系统


## 15. 性能原则

这是一个静态博客。

Astro build 后应主要生成：

    dist/
      index.html
      ...
      assets/

尽量减少客户端 JavaScript。

如果某个功能可以在 build time 完成，就不要在客户端运行。

避免为了简单 UI 功能引入大型 JS framework。


## 16. 部署目标

开发：

    Mac
      ↓
    VS Code
      ↓
    Astro
      ↓
    npm run dev

版本管理：

    Local Git
      ↓
    GitHub

部署：

    GitHub
      ↓
    Azure Linux VM
      ↓
    npm run build
      ↓
    dist/
      ↓
    Caddy
      ↓
    Internet

第一阶段允许直接通过 Azure Public IP 访问。

暂时不要求：

- Domain
- Cloudflare
- HTTPS domain configuration

后续再添加。


## 17. 第一版优先级

不要一开始实现所有功能。

第一阶段只完成：

1. Astro 项目初始化
2. 全局 Typography
3. Header
4. 首页
5. Markdown Blog
6. Article 页面
7. Light / Dark Mode
8. Responsive
9. 几篇示例文章

第一版完成后，应首先检查：

- 首页是否足够简洁
- 是否存在明显“模板感”
- 中文排版是否舒服
- 文章页面是否适合长时间阅读
- Dark Mode 是否舒服
- 手机端是否正常

确认视觉方向后，再添加 Archive / Tags / Search / RSS / Projects 等功能。


## 18. 最重要的设计约束

最终效果应处于：

    Coink
      ↓
    极简、个人化
      +
    AstroPaper
      ↓
    现代静态博客功能

之间。

不要向：

    Fuwari
    Stack
    Dashboard
    Card-heavy Blog

方向发展。

如果设计决策存在冲突：

> 优先减少元素，而不是增加元素。

如果一个边框、背景、卡片、动画不是必要的：

> 删除它。

网站的设计感主要来自：

> Typography + Spacing + Hierarchy + Color + Details

而不是 UI 组件数量。