# kailiu.me

Kai Liu 的个人网站。

基于 Astro 构建的静态网站，用于展示个人信息、技术项目、学习笔记与文章。

## 技术栈

- Astro
- TypeScript
- HTML / CSS
- Node.js 24
- npm
- Cloudflare Pages（计划部署）

## 本地开发

```bash
fnm use 24
npm ci
npm run dev
```

本地访问：

http://localhost:4321

## 生产构建

```bash
npm run build
```

构建结果输出至 `dist/`。

## 项目结构

- `src/components/`：公共组件
- `src/layouts/`：页面布局
- `src/pages/`：网站页面
- `src/styles/`：全局样式
- `public/`：静态资源

## 部署配置

- 网站：https://kailiu.me
- 平台：Cloudflare Pages
- 构建命令：`npm run build`
- 输出目录：`dist`
- Node.js：24

注意：Astro 新版本尚未正式发布到线上。

## 开发状态

目前已完成基础工程初始化、公共组件、
响应式首页和基础 SEO 配置。

内容页面与正式上线将在后续阶段完成。
