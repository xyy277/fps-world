<div align="center">

# 🎮 方块枪战 · Block FPS

**一个单文件、零安装、即开即玩的体素风第一人称射击游戏**
支持 PC 键鼠 + 移动端触屏 · 基于 Three.js

[![Play on GitHub Pages](https://img.shields.io/badge/Play-GitHub%20Pages-181717?style=for-the-badge&logo=github)](https://xyy277.github.io/fps-world/minecraft-fps.html)
[![Play on Cloudflare](https://img.shields.io/badge/Play-Cloudflare%20Pages-F38020?style=for-the-badge&logo=cloudflare)](https://fps-world.pages.dev/minecraft-fps.html)
[![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)](#-开源协议)
[![Single File](https://img.shields.io/badge/single%20file-HTML-22c55e?style=for-the-badge)](minecraft-fps.html)

**👆 点击上方按钮立即游玩，无需下载，无需安装**

</div>

---

## ✨ 游戏特色

> 我的世界风格 × 第一人称射击 × 波次生存，融在**一个 HTML 文件**里。

- 🌍 **程序化体素世界** —— 64×64×24 地形，含树木、岩石、掩体，开局即随机生成
- 🔫 **三种武器** —— 步枪（连发）/ 霰弹枪（近战爆发）/ 狙击枪（高倍瞄准镜），鼠标滚轮或按键快速切换
- 🧟 **波次生存** —— 丧尸与苦力怕轮番进攻，越往后越凶；清空一波回血 25
- 💥 **TNT 连锁引爆** —— 放置 TNT 一枪引爆，连锁爆炸清场丧尸，爽感拉满
- 🌗 **昼夜循环** —— 白天视野开阔，夜晚丧尸更狂暴，氛围与难度同步变化
- 🎯 **爆头双倍伤害** —— 命中头部金色 hitmarker，伤害翻倍
- ❤️ **掉落补给** —— 击杀敌人掉落红心（回血）与弹药，鼓励主动出击
- 🧱 **方块建造/破坏** —— 像我的世界一样放置与击碎方块，构建掩体或工事
- 🎨 **零资源依赖** —— 所有纹理用 Canvas 程序化生成，所有音效用 Web Audio 合成，无任何图片/音频文件
- 📱 **移动端原生触屏** —— 固定方向键 + 疾跑开关 + 滑动视角 + 动作按钮组，手机也能畅玩

## 🎮 操作方式

### PC 键鼠

| 按键 | 功能 | 按键 | 功能 |
|------|------|------|------|
| W A S D | 移动 | 鼠标 | 视角 |
| 左键 | 射击（击碎方块 / 引爆 TNT） | 右键 | 放置方块 |
| Q / 滚轮 | 切换武器 | F | 狙击瞄准镜 |
| 1 - 6 | 选择方块（6 = TNT） | R | 装填弹药 |
| Shift | 疾跑 | 空格 | 跳跃 |
| ESC | 暂停 | | |

### 移动端触屏

| 操作 | 功能 |
|------|------|
| ▲ ◀ ▼ ▶ | 左侧方向键移动（支持多指斜向） |
| 跑 | 点按切换疾跑 |
| 屏幕空白处滑动 | 转动视角 |
| 开火 / 跳 | 射击（按住连发）/ 跳跃 |
| 放 / 弹 / 枪 / 镜 | 放方块 / 装填 / 切武器 / 狙击镜 |
| 底部热键栏 | 点按选择方块（6 = TNT） |
| ⏸ | 左上角暂停 |

> 💡 提示：苦力怕靠近会自爆，优先点杀！TNT 连锁引爆是清场利器。

## 🚀 立即游玩

任选一个链接，浏览器打开即可：

| 平台 | 链接 | 特点 |
|------|------|------|
| GitHub Pages | https://xyy277.github.io/fps-world/minecraft-fps.html | 与代码仓库同步，推送即更新 |
| Cloudflare Pages | https://fps-world.pages.dev/minecraft-fps.html | 全球 CDN 加速，访问更快 |

## 💻 本地运行

无需任何构建步骤，三种方式任选其一：

```bash
# 方式一：直接双击文件
直接用浏览器打开 minecraft-fps.html

# 方式二：本地静态服务器（推荐，避免某些浏览器限制）
npx serve .
# 或
python -m http.server 8000
```

## 🛠 技术栈

| 层 | 技术 | 说明 |
|----|------|------|
| 渲染引擎 | [Three.js r128](https://threejs.org/) | 通过 CDN 引入，不打包 |
| 实现语言 | 原生 HTML / CSS / JavaScript | 无框架、无编译、无依赖 |
| 纹理 | Canvas 2D API | 程序化生成像素纹理 |
| 音频 | Web Audio API | 程序化合成音效 |
| 部署 | GitHub Pages + Cloudflare Pages | 纯静态托管 |

**为什么单文件？** —— 极致的「即开即玩」体验：一个链接发给朋友就能玩，无需安装、无需登录、无需后端。整个游戏（含逻辑、渲染、纹理、音效）压缩在**一个 HTML 文件**里，约 1450 行代码。

## 📂 项目结构

```
fps-world/
├── minecraft-fps.html   # 游戏本体（单文件）
├── README.md            # 本文档
├── AGENTS.md            # 多 Agent 协作开发规则
├── .gitignore           # 忽略 .env 等敏感文件
└── .env.example         # 密钥字段占位模板
```

## 🤝 参与贡献

欢迎贡献！无论是修复 bug、优化玩法、改进触屏体验，还是新增武器/敌人类型。

1. Fork 本仓库
2. 创建分支：`git checkout -b feat/your-feature`
3. 提交更改：`git commit -m "feat: 添加 XXX"`
4. 推送分支：`git push origin feat/your-feature`
5. 发起 Pull Request

> 多 Agent / AI 协作开发请先阅读 [AGENTS.md](AGENTS.md)，了解角色分工与编码规范。

## 🗺 路线图

- [ ] 更多武器（手枪、火箭筒）
- [ ] 更多敌人类型（骷髅弓箭手、蜘蛛）
- [ ] Boss 战
- [ ] 排行榜（本地存储）
- [ ] 可选存档
- [ ] 更多地形生物群系

## 📜 开源协议

MIT License —— 可自由使用、修改、分发。打出你的星星 ⭐ 就是最大的鼓励！

---

<div align="center">

**如果这个游戏让你玩得开心，给个 ⭐ Star 支持一下！**

Made with ❤️ and Three.js

</div>
