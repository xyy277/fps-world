# AGENTS.md — 方块枪战 多 Agent 协作开发规则

> 本文件是所有 AI Agent（及人类协作者）在本仓库工作的**唯一行为准则**。
> 任何 Agent 在动手前必须完整阅读本文件，并在整个会话中严格遵守。
> 修改本文件需经仓库所有者确认。

---

## 1. 项目使命与范围

- **项目**：方块枪战（Block FPS）—— 单页、零依赖安装、即开即玩的体素风第一人称射击游戏。
- **目标平台**：现代浏览器（PC + 移动端触屏），无需后端、无需登录、无需下载。
- **发布渠道**：GitHub Pages + Cloudflare Pages 双部署，任一链接可直接游玩。
- **核心约束**：必须保持「单 HTML 文件、CDN 加载 Three.js、开箱即玩」的形态。新增功能不得破坏这一形态。

## 2. 技术栈

| 层 | 技术 | 说明 |
|----|------|------|
| 渲染 | Three.js r128 | 通过 CDN `<script>` 引入，不走 npm/bundler |
| 语言 | 原生 HTML/CSS/JS（ES5+ 风格） | 不引入编译步骤、不引入框架 |
| 音频 | Web Audio API | 程序化合成，无音频文件 |
| 纹理 | Canvas 2D 程序化生成 | 无图片资源 |
| 部署 | GitHub Pages + Cloudflare Pages | 静态托管 |
| 凭证 | `.env`（本地，**不提交**） | 含 GitHub Token、Cloudflare Token |

## 3. 仓库结构

```
fps-world/
├── minecraft-fps.html   # 游戏本体（单文件，约 2600 行）
├── README.md            # 英文主文档（GitHub 国际化推广）
├── README.zh-CN.md      # 中文文档
├── AGENTS.md            # 本文件，多 Agent 开发规则
├── docs/                # 研究与进度文档
│   ├── fps-capability-research.md   # 单页 FPS 功能上限调研报告
│   └── implementation-progress.md   # 实施进度与后续目标
├── .github/workflows/   # CI：Cloudflare Pages 自动部署
├── .gitignore           # 忽略 .env 等敏感文件
├── .env                 # 本地密钥（被 .gitignore 排除，绝不提交）
└── .env.example         # 密钥占位模板（可提交，供协作者参考字段）
```

## 4. Agent 角色与协作协议

多 Agent 并行开发时，按角色分工。每个 Agent 在会话开始时声明自己的角色。

| 角色 | 职责 | 可修改的文件 |
|------|------|------------|
| **@ gameplay** | 玩法逻辑：武器、敌人、波次、AI、伤害、掉落 | `minecraft-fps.html` 的逻辑区段 |
| **@ render** | 渲染、体素网格、纹理、粒子、光照、昼夜 | `minecraft-fps.html` 的渲染区段 |
| **@ ui-ux** | HUD、菜单、触屏控件、响应式、可访问性 | `minecraft-fps.html` 的 HTML/CSS 区段 |
| **@ infra** | 部署、CI、密钥、git、GitHub Pages、Cloudflare | `.gitignore`、部署脚本、`README.md`、`AGENTS.md` |
| **@ docs** | 文档同步、README、AGENTS、changelog | 文档类文件 |

### 协作铁律
1. **先读后改**：修改任何文件前，必须先 `Read` 该文件相关区段，理解上下文。
2. **单文件冲突防护**：因为游戏是单 HTML 文件，多 Agent 同时改它极易冲突。规则：
   - 改动前在 todo 中标注「待改区段行号范围」。
   - 同一会话内，同一文件由一个 Agent 串行推进，不并行写。
   - 跨 Agent 改同文件时，后改者必须基于最新磁盘内容 re-read。
3. **最小改动原则**：只改被要求的部分，不顺手重构、不扩大范围。
4. **不引入新依赖**：除非所有者明确同意，不新增 CDN 库、不引入 bundler。
5. **声明角色**：每次会话首条消息声明 `角色：@xxx`，便于协作者识别。

## 5. 编码规范

- **语言**：注释与面向用户文本使用**中文**（与游戏 UI 一致）；变量名、函数名用英文。
- **风格**：保持现有风格——`const`/`function` 声明、双引号字符串、`"use strict"`、区段用 `// ---- 标题 ----` 分隔。
- **体素/世界常量**：`W/D/H`、`CHUNK` 等全局常量集中在「基础常量」区段，不要散落。
- **触屏适配**：任何新增交互都必须同时考虑 PC 鼠标键盘与移动端触屏两套输入。
- **性能**：移动端优先，新增渲染逻辑需注意 draw call 与粒子数量。
- **无构建步骤**：禁止引入需要 `npm install` 才能运行的流程；CDN 资源需在 README 中登记版本。

## 6. 安全与密钥规则（最高优先级）

1. **`.env` 永不提交**：`.gitignore` 必须始终排除 `.env`、`.env.*`、`.dev.vars`、`*.local`。
2. **密钥不入代码**：GitHub Token、Cloudflare Token、Account ID 不得硬编码进任何会提交的文件。需要时从 `.env` 读取。
3. **部署用密钥**：仅由 `@infra` Agent 在本地执行部署命令时使用，不写入仓库。
4. **泄露处置**：一旦怀疑密钥被提交，立即停止、通知所有者轮换密钥，并清理 git 历史。
5. **`.env.example`**：只放字段名占位（如 `GITHUB_TOKEN=`），不放真实值。
6. **会话内密钥**：Agent 在会话中读到的真实密钥，**不得**回显在会被提交的文件或 commit message 中。

## 7. 部署规则

### 7.1 GitHub Pages
- 仓库：`xyy277/fps-world`（公开）。
- Pages 来源：`main` 分支根目录（单 HTML 文件直接托管）。
- 入口：`minecraft-fps.html`（通过 README 顶部「在线游玩」按钮链接）。
- 推送 `main` 即自动更新 Pages，无需额外 CI。

### 7.2 Cloudflare Pages
- 项目名：`fps-world`。
- 构建命令：无（纯静态单文件）。
- 输出目录：仓库根目录。
- 部署方式：`wrangler pages deploy` 或 Cloudflare API。
- Account ID 与 Token 从 `.env` 读取，不进仓库。

### 7.3 部署顺序（@infra 执行）
1. 确认 `.gitignore` 已排除 `.env`。
2. `git init` → 创建仓库 → `git push -u origin main`。
3. 启用 GitHub Pages（main 分支）。
4. `wrangler pages deploy` 到 Cloudflare。
5. 将两个在线链接写入 `README.md` 顶部。
6. 验证两个链接可正常加载并进入游戏。

## 8. 测试与验证

- **无自动化测试**：本项目不引入测试框架。
- **人工验证**：每次改动后，`@infra` 或改动者 Agent 应：
  1. 本地用浏览器打开 `minecraft-fps.html` 确认无 JS 控制台报错。
  2. 在移动端视口（如 DevTools 设备模式）确认触屏控件可用。
  3. 推送后访问 Pages 链接确认在线可玩。
- **回归点**：改动武器/敌人/触屏控件后，重点回归对应玩法。

## 9. 文档同步

- `@docs` Agent 负责保持 README、AGENTS、changelog 与代码同步。
- 新增功能 → 同步更新 README「功能特性」区段。
- 流程/规则变化 → 同步更新 AGENTS.md。
- 用户偏好记录在 TRAE memory（`project_memory.md`），跨会话保持一致。

## 10. Git 提交规范

- Commit message 用中文，简洁描述「为什么」改。
- 不自动 commit，除非所有者明确要求。
- 不自动 push，除非所有者明确要求。
- 不使用 `git add -A`，按文件名精确添加，避免误带 `.env`。

## 11. 禁止事项

- ❌ 提交 `.env` 或任何含真实密钥的文件。
- ❌ 未经同意引入 npm/bundler/框架/新 CDN 依赖。
- ❌ 拆分单 HTML 文件为多文件（除非所有者明确要求）。
- ❌ 自动执行 `git push --force`、`reset --hard` 等破坏性操作。
- ❌ 在 commit message 或代码中回显真实密钥。
- ❌ 删除用户已有的、仍在使用的代码而不确认。
