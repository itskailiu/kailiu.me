# kailiu.me 网站工程存档与续建说明

**归档日期：** 2026-10-15（北京时间）  
**项目定位：** 个人身份展示、学习记录与技术成果的长期入口  
**归档阶段：** Astro 基础工程完成，GitHub → Cloudflare Pages 自动部署已打通；内容建设尚未开始  
**注意：** 本文是项目交接档案，不包含本地完整源码；源码以 Git 仓库为准。

## 1. 工程与仓库

- **本地路径：** `~/Developer/kailiu.me`
- **GitHub 仓库：** `kailiudev/kailiu.me`
- **开发及当前新版部署分支：** `feat/astro`
- **旧分支：** `main`（仍需在适当时候与 Astro 版本整理合并）
- **最后已核实的工程提交：** `c6041e8` — `refactor: finalize Astro site foundation`
- **此前提交：** `be74c8e` — Astro 初始化；`db30c14` — 响应式首页。
- 最后一次提交时工作区干净。此后曾将临时 `kailiu-astro-starter` 目录移动进项目，再移除；**移除后的 Git 状态尚未复查**。

## 2. 技术选型和部署方式

| 项目 | 当前选择 |
|---|---|
| 框架 | Astro 7.3.8 |
| Node.js | 24（本地已核验 v24.21.0，使用 fnm） |
| 包管理 | npm，提交 `package-lock.json` |
| 渲染 | 静态生成（`output: 'static'`） |
| 构建 | `npm run build` |
| 输出 | `dist/` |
| 代码托管 | GitHub |
| 网站部署 | Cloudflare Pages，Git 集成自动构建 |
| 框架底座 | Astro + HTML/CSS；目前无数据库、CMS、登录或独立服务端 |

Astro 配置中已设置 `site: 'https://kailiu.me'`。在该项目的 `feat/astro` 分支推送新提交后，当前 Pages 新项目会自动重新部署。

## 3. 已完成的网站结构

```text
~/Developer/kailiu.me/
├── .git/                      Git 历史与本地分支（隐藏）
├── .gitignore                 忽略依赖、缓存与本地辅助文件
├── .node-version              24
├── astro.config.mjs           site 与静态输出
├── package.json               npm 命令与依赖
├── package-lock.json          依赖锁定
├── tsconfig.json              TypeScript 配置
├── README.md                  项目说明
├── index.html                 旧版“旺铺招租”占位页（遗留）
├── public/
│   ├── favicon.svg            当前临时蓝底白色 K 标识
│   └── favicon.ico            原模板图标（待统一）
├── src/
│   ├── components/
│   │   ├── Header.astro       公共导航
│   │   └── Footer.astro       公共页脚
│   ├── layouts/
│   │   └── BaseLayout.astro   HTML 外壳、公共组件、SEO
│   ├── styles/
│   │   └── global.css         基础全局样式
│   └── pages/
│       └── index.astro        目前唯一正式 Astro 页面
├── dist/                      构建输出，可重建、已忽略
└── node_modules/              依赖，可重装、已忽略
```

说明：本地还可能有 `.idea/`、`.vscode/`、`AGENTS.md`、`CLAUDE.md` 等编辑器或模板辅助文件，后几项已按此前约定从 Git 跟踪范围排除。临时项目 `kailiu-astro-starter` 曾用于初始化和测试；用户已将其从 `kailiu.me` 内移除，不应继续依赖。

## 4. 当前页面与视觉（均是可修改的初版设计）

- 首页主标题：**保持好奇，持续构建。**
- 展示名：**Kai Liu**；中文为主、英文为辅。
- 页面包含顶部导航、个人介绍、正在学习卡片、三个方向卡片和页脚。
- 基调：暖白背景 `#fafaf8`、蓝色强调 `#4268d6`、深色正文 `#172033`。
- 最大内容宽度约 `1120px`，手机断点约 `760px`，PC 与模拟移动端都已做过初步检查。
- 导航大部分仍是页内锚点；**About、Notes、Projects、Blog 独立页面尚未创建**。
- 完成的基础 SEO：description、canonical、Open Graph 标题/描述/网址、Twitter Card、主题色、SVG favicon；已从 `dist/index.html` 实际核对输出。
- 尚未配置：真实内容体系、sitemap、社交分享图片、正式品牌视觉、全面无障碍/跨设备验收。

## 5. Cloudflare 环境与域名迁移

**新项目：** `kailiu-me`  
**新版公网地址：** https://kailiu-me-1hh.pages.dev  
**GitHub 集成：** `kailiudev/kailiu.me`；Cloudflare 生产分支当前设为 `feat/astro`  
**最后已核实部署提交：** `c6041e8`，部署状态成功，用户已确认新版公网地址可打开。

**旧项目：** `me`  
**旧版地址：** https://kailiu-me.pages.dev  
**旧页面内容：** “旺铺招租”原生 HTML 占位页。此前正式域名 `kailiu.me` 指向此旧版，并曾在旧项目中占用自定义域绑定。旧项目与新项目均出现在同一个 Cloudflare 账户，且都显示关联同一 GitHub 仓库；旧项目应暂时保留，避免误删。

**正式域名：** https://kailiu.me  
用户已开始从旧项目解绑并在新项目中添加自定义域，**最后得知的状态是 Cloudflare 正在验证，尚未获得“Active”和正式域名显示新版页面的最终确认**。不要将其写成已验收成功。

**邮箱：** Cloudflare Email Routing 的 MX、SPF、DKIM 等相关记录需要保留，不应因切换网站而删除。

## 6. 下次启动开发的命令

```bash
cd ~/Developer/kailiu.me
fnm use 24
node -v
git status -sb
git log -3 --oneline
npm run dev
```

浏览器访问 `http://localhost:4321/`。需要生产构建时运行 `npm run build`。`node_modules` 不存在或缺少依赖时才运行 `npm ci`。开发服务器用 `Ctrl+C` 停止。

## 7. 下次优先检查的事项

1. 确认 Cloudflare 新项目 `kailiu-me` 的 `kailiu.me` 自定义域显示 **Active**；访问正式域名应为 Astro 新首页且 HTTPS 正常。
2. 核对 DNS 中根域名的网页记录已指向新项目，邮件相关 MX/TXT 记录仍在且转发正常。
3. `git status -sb` 确认移动临时文件夹后无意外的未跟踪文件；必要时检查 `find . -maxdepth 2 -type d`。
4. 明确长期分支规范：当前新版以 `feat/astro` 为 Pages 生产分支，未来视情况合并到 `main` 并切换；**变更前确认两个 Cloudflare 项目的自动部署规则**。
5. 旧 `index.html`、模板 `favicon.ico`、旧 Pages 项目 `me` 均可在确认没有依赖之后再整理；暂不擅自删除。

## 8. 下一阶段（尚未执行）

先与用户确认信息架构、网站定位和公开内容范围，再建设 About、Notes、Projects、Blog 和 Contact。之后再考虑正式品牌视觉、移动导航、站点地图及其他 SEO 优化。`kailiu.dev` 作为独立技术空间，暂未进入建设。

**原则：** 不要为了堆功能引入 React、数据库、登录和 CMS；优先保持 Astro 静态站的简单和长期可维护性。不要把当前示例文案视为最终个人品牌定位。

## 9. 真正的源码备份方法（在用户 Mac 终端执行）

以下命令不会修改当前项目，只会在桌面输出两个备份文件：

```bash
cd ~/Developer/kailiu.me
# 备份最后已核实提交的可追踪源码（不包含依赖和构建产物）
git archive --format=zip --output="$HOME/Desktop/kailiu.me-source-2026-10-15.zip" c6041e8
# 备份当前本地仓库的 Git 历史、分支和引用
git bundle create "$HOME/Desktop/kailiu.me-git-2026-10-15.bundle" --all
# 验证 Git 历史备份可以被读取
git bundle verify "$HOME/Desktop/kailiu.me-git-2026-10-15.bundle"
```

`.zip` 是可还原源码的快照，`.bundle` 可用于恢复 Git 历史。它们都不是云端自动持续备份：以后产生新提交，需要重新生成。GitHub 远端仓库仍是日常同步副本。

## 10. 下次交接提示词

> 继续建设我的 `kailiu.me` 个人网站。请先根据《kailiu.me 网站工程存档与续建说明》接续，不要重新安装环境或创建仓库。当前 Astro 基础工程已完成，GitHub 和 Cloudflare Pages 自动部署已打通，最新确认提交是 `c6041e8`；正式域名迁移上次仍在验证。先检查域名和 Git 状态，再和我一起确认信息架构后开始内容建设。一次只推进一小步，保留已有源码和部署。
