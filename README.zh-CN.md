<div align="center">

# 🎮 方块枪战 · Block FPS

**一个单文件、零安装、即开即玩的体素风第一人称射击游戏**
支持 PC 键鼠 + 移动端触屏 · 基于 Three.js

[![Play on GitHub Pages](https://img.shields.io/badge/Play-GitHub%20Pages-181717?style=for-the-badge&logo=github)](https://xyy277.github.io/fps-world/minecraft-fps.html)
[![Play on Cloudflare](https://img.shields.io/badge/Play-Cloudflare%20Pages-F38020?style=for-the-badge&logo=cloudflare)](https://fps-world.pages.dev/minecraft-fps.html)
[![View on GitHub](https://img.shields.io/badge/View-GitHub-181717?style=for-the-badge&logo=github)](https://github.com/xyy277/fps-world)
[![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)](#-开源协议)
[![Single File](https://img.shields.io/badge/single%20file-HTML-22c55e?style=for-the-badge)](minecraft-fps.html)
[![Lines of Code](https://img.shields.io/badge/lines-2600+-orange?style=for-the-badge)](minecraft-fps.html)

**👆 点击上方按钮立即游玩，无需下载，无需安装**

**简体中文** · [English](README.md)

</div>

---

## 📸 游戏截图

<div align="center">

![方块枪战封面](docs/screenshots/hero-banner.jpg)

*白天体素战场 —— 树木、方块、逼近的敌人*

![夜间战斗场景](docs/screenshots/night-combat.jpg)

*夜间战斗 —— 雨幕、火把光、狙击镜、伤害数字*

</div>

---

## 📑 目录

- [✨ 游戏特色](#-游戏特色)
- [🎮 操作方式](#-操作方式)
- [🚀 立即游玩](#-立即游玩)
- [💻 本地运行](#-本地运行)
- [🛠 技术栈](#-技术栈)
- [📂 项目结构](#-项目结构)
- [🤝 参与贡献](#-参与贡献)
- [🗺 路线图](#-路线图)
- [📜 开源协议](#-开源协议)

---

## ✨ 游戏特色

> 我的世界风格 × 第一人称射击 × 波次生存，融在**一个 HTML 文件**里。

### 世界与渲染
- 🌍 **程序化体素世界** —— 64×64×24 地形，含树木、岩石、掩体，开局即随机生成
- 🌗 **昼夜循环** —— 白天视野开阔，夜晚丧尸更狂暴，氛围与难度同步变化
- 🌧 **动态天气** —— 雨/雪粒子系统，与昼夜联动随机切换（晴/雨/雪）
- 🎨 **零资源依赖** —— 所有纹理用 Canvas 程序化生成，所有音效用 Web Audio 合成，无任何图片/音频文件
- ✨ **后处理泛光** —— 高画质下 ACES Filmic 色调映射，电影感画面（可开关）

### 战斗与武器
- 🔫 **三种武器** —— 步枪（连发）/ 霰弹枪（近战爆发）/ 狙击枪（高倍瞄准镜），鼠标滚轮或按键快速切换
- 💥 **后坐力 + 动态散布** —— 连发增大、停火恢复；换弹动画枪身下沉旋转
- 💣 **手雷 + TNT** —— 手雷抛物线物理投掷；放置 TNT 一枪引爆，连锁爆炸清场
- 🗡 **近战攻击** —— 扇形命中判定 + 冷却，近战利器
- 🎯 **爆头双倍伤害** —— 命中头部金色 hitmarker，伤害翻倍
- ❤️ **掉落补给** —— 击杀敌人掉落红心（回血）与弹药，鼓励主动出击

### 敌人与 AI
- 🧟 **波次生存** —— 丧尸与苦力怕轮番进攻，越往后越凶；清空一波回血 25
- 🧠 **FSM 敌人 AI** —— 状态机（追击/攻击/逃跑/游荡）+ A* 寻路（10×10 网格，500 迭代上限）
- 🛡 **掩体与预判** —— 敌人利用掩体，预判玩家移动

### 进度与存档（RPG 化）
- 💾 **持久存档** —— localStorage 存最高分/最高波次/总击杀/总局数/总爆头/最佳连杀
- 🏆 **12 项成就** —— 局内实时检测 + Toast 通知 + 成就墙（初次猎杀 → 传奇）
- 📈 **经验与等级** —— 击杀 +10xp、清波 +20xp，升级获技能点
- ⬆ **升级树** —— 4 项属性 × 5 级，全部实际影响玩法：
  - 伤害 +10%/级（子弹与近战）
  - 最大生命 +15/级（替代硬编码 100）
  - 换弹速度 -10%/级
  - 移动速度 +8%/级

### 音频
- 🎵 **程序化 BGM** —— 三段循环旋律（菜单/战斗/结算），Oscillator+GainNode 合成，8-bit chiptune 风格
- 🔊 **完整 SFX** —— 枪声、爆炸、脚步、换弹、击中、UI 点击，全部合成
- 🔇 **默认静音** —— 首次进入无声（避免惊吓），可在设置打开，跨会话记忆

### UI 与反馈
- 🎯 **动态准星** —— 随散布扩大
- 💬 **伤害数字** —— DOM 池 + 3D→2D 投影 + 上浮淡出，爆头金色/暴击红色
- 📋 **击杀提示** —— 最近 5 条，自动淡出
- 🗺 **小地图** —— Canvas 2D，每 3 帧刷新，显示玩家视野/敌人/掉落
- 📊 **计分板** —— 局末表格，武器分布/爆头数/最高连杀
- ⚙ **设置面板** —— 画质/音量/灵敏度 + 5 开关（静音/BGM/天气/纹理/后处理），全部记忆

### 操作与平台
- 🖥 **PC 键鼠** —— 完整按键映射 + Pointer Lock + 滚轮切武器
- 📱 **移动端原生触屏** —— 固定方向键 + 疾跑开关 + 滑动视角 + 动作按钮组（开火/跳/放/弹/枪/镜/雷/刀）
- 🎮 **首次教程** —— 首次开始游戏显示操作指引（6 秒淡出），PC/触屏双版本

## 🎮 操作方式

### PC 键鼠

| 按键 | 功能 | 按键 | 功能 |
|------|------|------|------|
| W A S D | 移动 | 鼠标 | 视角 |
| 左键 | 射击（击碎方块 / 引爆 TNT） | 右键 | 放置方块 |
| Q / 滚轮 | 切换武器 | F | 狙击瞄准镜 |
| 1 - 6 | 选择方块（6 = TNT） | R | 装填弹药 |
| Shift | 疾跑 | 空格 | 跳跃 |
| G | 手雷 | V | 近战 |
| ESC | 暂停 | | |

### 移动端触屏

| 操作 | 功能 |
|------|------|
| ▲ ◀ ▼ ▶ | 左侧方向键移动（支持多指斜向） |
| 跑 | 点按切换疾跑 |
| 屏幕空白处滑动 | 转动视角 |
| 开火 / 跳 | 射击（按住连发）/ 跳跃 |
| 放 / 弹 / 枪 / 镜 / 雷 / 刀 | 放方块 / 装填 / 切武器 / 狙击镜 / 手雷 / 近战 |
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
| 音频 | Web Audio API | 程序化合成 SFX + BGM |
| 存档 | localStorage | 版本化 JSON，持久化进度 |
| 部署 | GitHub Pages + Cloudflare Pages | 静态托管，GitHub Actions 双部署 |

**为什么单文件？** —— 极致的「即开即玩」体验：一个链接发给朋友就能玩，无需安装、无需登录、无需后端。整个游戏（逻辑 + 渲染 + 纹理 + 音效 + 进度）压缩在**一个 HTML 文件**里，约 2600 行代码。

## 📂 项目结构

```
fps-world/
├── minecraft-fps.html   # 游戏本体（单文件，约 2600 行）
├── README.md            # 英文文档（主）
├── README.zh-CN.md      # 本中文文档
├── AGENTS.md            # 多 Agent 协作开发规则
├── docs/                # 研究与进度文档
│   ├── fps-capability-research.md   # 单页 FPS 功能上限调研
│   ├── implementation-progress.md   # 实施进度与路线图
│   └── screenshots/                 # README 展示截图
├── .github/workflows/   # CI：Cloudflare Pages 自动部署
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

**已完成（P0-P5）**
- [x] 架构与性能护栏（画质分级 + 对象池）
- [x] 武器手感（后坐力 + 动态散布 + 换弹动画 + 手雷 + 近战）
- [x] 敌人 AI（FSM 状态机 + A* 寻路 + 掩体预判）
- [x] 战斗 UI（伤害数字 + 小地图 + 击杀提示 + 计分板 + 设置）
- [x] 存档与进度系统（localStorage + 12 成就 + 升级树）
- [x] 沉浸感增强（程序化 BGM + 天气 + 后处理 + 教程 + 5 开关）

**规划中（P6-P7）**
- [ ] 更多武器（手枪、火箭筒）
- [ ] 更多敌人类型（骷髅弓箭手、蜘蛛）
- [ ] Boss 战
- [ ] 主动技能（冲刺 / 护盾 / 时停）
- [ ] 排行榜（本地存储）
- [ ] PWA 离线游玩 + 多语言 + 手柄支持
- [ ] 更多地形生物群系

> 详细调研与进度见 [docs/](docs/)。

## 📜 开源协议

MIT License —— 可自由使用、修改、分发。打出你的星星 ⭐ 就是最大的鼓励！

---

<div align="center">

**如果这个游戏让你玩得开心，给个 ⭐ Star 支持一下！**

Made with ❤️ and Three.js

</div>
