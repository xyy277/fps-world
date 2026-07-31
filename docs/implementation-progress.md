# 实施进度与后续目标

> 更新时间：2026-07-31
> 当前代码规模：3363 行（minecraft-fps.html）
> 本地领先 origin/main：2 个 commit（未 push）

---

## 1. 总体状态

| 维度 | 状态 |
|------|------|
| 架构与性能护栏（P0） | ✅ 已完成 |
| 武器手感与扩展（P1A/P1B） | ✅ 已完成 |
| 敌人 AI（P2） | ✅ 已完成 |
| 战斗 UI 与反馈（P3） | ✅ 已完成 |
| 存档与进度系统（P4） | ✅ 已完成 |
| 沉浸感增强（P5） | ✅ 已完成 |
| 内容扩展（P6） | ✅ 已完成（P6.1-P6.5 全部落地） |
| 画质增强（P7） | ✅ 已完成（光照/雾化/InstancedMesh/纹理细化） |
| 多场景/关卡（P8） | 🔄 进行中（P8.1/P8.2/P8.3 已完成，P8.4 待提交） |
| 体验打磨（P9） | ⏳ 待启动 |
| GitHub Pages 部署 | ✅ 在线（落后本地 2 commit） |
| Cloudflare Pages 部署 | ✅ 在线（落后本地 2 commit） |
| 双部署自动同步（Actions） | ✅ 已配置 |

**阶段结论**：P0-P7 全部落地，游戏具备完整单局循环 + 长期进度 + 视听反馈 + 多武器多敌人 + Boss 战 + 主动技能 + 画质增强。P8 多场景/关卡系统进行中（biome 切换 + 关卡递进 + 通关奖励已完成），P9 体验打磨为后续阶段。

---

## 2. 已完成 Phase 详表

### P0：架构与性能护栏
- commit：`a12a308`
- 画质分级（低/中/高）：动态调整雾、阴影、粒子数
- 对象池：粒子与弹道复用，减少 GC
- 区块按需构建

### P1A：武器手感增强
- commit：`ca75c15`
- 后坐力 + 动态散布（bloom）：连发增大、停火恢复
- 换弹动画：枪身下沉旋转 + 弹药计数
- 弹壳抛出

### P1B：武器扩展
- commit：`5c07039`
- 手雷（G 键 / 触屏「雷」按钮）：抛物线物理 + 落地引爆，**初始 3 颗，击杀掉落补充（非无限）**
- 近战（V 键 / 触屏「刀」按钮）：扇形命中 + 冷却

### P2：敌人 AI 升级
- commit：`e69e834`
- FSM 状态机：追击 / 攻击 / 逃跑 / 游荡
- A* 寻路：10×10 网格 + 500 迭代上限
- 掩体利用 + 玩家速度预判

### P3：战斗 UI 与反馈
- commit：`221230d`
- 伤害数字：DOM 池 + 3D→2D 投影 + 上浮淡出，爆头金色/暴击红色
- 小地图：Canvas 2D，每 3 帧刷新，显示玩家视野/敌人/掉落
- 击杀提示（Killfeed）：限定 5 条，自动淡出
- 计分板：武器分布 + 爆头数 + 最高连杀
- 设置面板：画质 / 音量 / 灵敏度，localStorage 记忆

### P4：存档与进度系统
- commit：`f58e8b3`
- localStorage 全局存档：最高分/最高波次/总击杀/总局数/总爆头/最佳连杀
- 12 项成就：局内实时检测 + Toast 通知 + 成就墙
- XP / 等级 / 技能点：升级公式 `lv * 100`，击杀 +10xp、每波 +20xp
- 升级树：4 项属性（伤害/血量/换弹/移速）各 5 级，玩法实际生效
- UI 入口：菜单 / 暂停 / 游戏结束界面均加入「进度」「升级」按钮

### P5：沉浸感增强
- commit：`21b4b17`
- 程序化 BGM：三段循环旋律（menu/battle/over），Oscillator+GainNode 序列播放
- 默认静音 + 设置面板扩展：5 开关（静音/BGM/天气/纹理/后处理）
- 天气系统：雨/雪 Points 粒子，与昼夜联动随机切换
- 后处理泛光：ACESFilmic toneMapping 近似
- 教程引导：首次开始游戏显示操作指引（PC/触屏双版本），6 秒淡出

### P6.1：武器扩展（内容扩展第一阶段）
- commit：`1370be6`
- 新增手枪：初始武器，低伤害高精度（dmg 22 / mag 12 / rate 0.28）
- 新增火箭筒：范围爆破（dmg 120 / splash 4.5），复用 TNT 爆炸特效与范围伤害逻辑
- WORDER 扩展为 5 把武器：pistol / rifle / shotgun / sniper / rocket
- 初始武器改为手枪（cur = "pistol"）
- 新增 pistol / rocket 音效

### P6.2：敌人扩展（内容扩展第二阶段）
- commit：`1370be6`
- 新增骷髅弓箭手：远程射击，距离越近命中率越高（上限 70%），2.2s 射击间隔，12 点伤害
- 新增蜘蛛：快速近战（speed 3.2），可跳跃突进（4-8 距离触发，4s 冷却），0.8s 攻速
- 敌人属性差异化：hp/headY/height/speed 集中管理
- spawnMob 按波次解锁：zombie(1+) / creeper(2+) / spider(3+) / skeleton(4+)
- 新增 buildSkeletonModel / buildSpiderModel 模型构建

### P6.3：Boss 战
- 每 5 波出现 Boss（僵尸王），三阶段（100%/60%/30% HP 切换）
- 阶段技能：冲撞（高速突进）、召唤（生成 3 只小怪）、范围攻击（AOE）
- Boss 血条 HUD（顶部居中，显示阶段）
- 血量随波次 + 关卡双重递增：`(800 + floor(wave/5)*400) * (1 + (level-1)*0.3)`

### P6.4：主动技能系统
- 三技能：冲刺（E，1.5s 加速 50%，8s CD）、护盾（Z，4s 减伤 70%，15s CD）、时停（X，3s 敌人移速×0.2，25s CD）
- 时停影响敌人/手雷/掉落物（timeScale），玩家与粒子不受影响
- 触屏底部技能栏（3 圆形按钮 + conic-gradient 冷却覆盖）
- PC 模式默认隐藏技能栏，键盘 E/Z/X 触发

### P6.5：操作优化 + 浏览器验证
- 右键改为 ADS 瞄准射击（所有武器，FOV 75→45，散布减半）
- 建造方块改键：C 键 / 鼠标中键（释放 E 给主动技能）
- F 键保留狙击专属高倍镜（FOV→15）

### P7：画质增强（程序化路线，零素材）
- P7.1 光照升级：DirectionalLight + ShadowMap + 暖色 HemisphereLight，太阳/阴影相机跟随玩家
- P7.2 雾化纵深：Fog 参数按 biome 联动（草地蓝雾 / 沙漠黄雾 / 雪原白雾 / 废墟褐雾）
- P7.3 植被 InstancedMesh：草丛/远景山脉批量渲染，instanceColor 按 biome 着色
- P7.4 纹理细化：Canvas 2D 加噪声/划痕/污渍，方块材质细节提升

### P8.1：Biome 数据结构 + genWorld 参数化
- 4 种 biome：草地（grassland）/ 沙漠（desert）/ 雪原（snow）/ 废墟（ruins）
- 每 biome 独有参数：地面/地下方块、高度图、装饰物（树/仙人掌/枯树/废墟柱）、天空/雾色
- applyBiome() 切换天空色、雾色、光照色调
- genWorld() / buildGrass() / buildDistantMountains() 全部读取 biome 参数

### P8.2：关卡切换器 + 难度递进
- 5 波为一关，通关后 level++ 并切换至下一 biome（BIOME_ORDER 循环）
- 难度递进：敌人 HP ×(1 + (level-1)*0.25)，速度 +(level-1)*0.15
- Boss 血量随关卡额外 ×(1 + (level-1)*0.3)
- 通关时重新生成地形（genWorld + buildGrass + buildDistantMountains + buildAllChunks）
- HUD 显示「关卡 N · 波次 M」

### P8.3：通关奖励系统
- 每 5 波通关弹出奖励选择面板（3 选 1，本局永久累积）
  - ❤️ 战地急救：回满生命 + 25 最大生命
  - ⚔️ 火力强化：+8% 伤害（累积）
  - 💨 风之疾走：+8% 移速（累积）
- 奖励面板打开时暂停游戏（state→paused + rewardOpen 标记阻断波次推进）
- 选择后恢复游戏 + 重新锁定鼠标 + 5s 准备时间
- runBuffs 纳入 getUpgradedStats()，与存档升级乘算叠加
- startGame 重置 level/runBuffs/rewardOpen；gameOver 清除面板状态

---

## 3. 部署状态

| 平台 | 地址 | 状态 |
|------|------|------|
| GitHub Pages | https://xyy277.github.io/fps-world/minecraft-fps.html | ✅ 在线（落后本地 2 commit） |
| Cloudflare Pages | https://fps-world.pages.dev/minecraft-fps.html | ✅ 在线（落后本地 2 commit） |
| 自动同步 | GitHub Actions `deploy-cloudflare.yml` | ✅ push 即双部署 |

> 注：本地领先 2 个 commit（`9494a31` docs + `1370be6` P6.1/P6.2），P6.3-P8.3 尚未 commit。push 后将自动触发双平台更新。

---

## 4. 后续目标（按优先级收敛）

### 4.1 P8 剩余：多场景/关卡收尾

| 编号 | 功能 | 说明 | 优先级 |
|------|------|------|--------|
| P8.4 | 浏览器验证 + commit + 文档同步 | 人工回归 P8 全部内容（biome 切换/关卡递进/通关奖励），确认无报错后提交 | 🔴 高 |

### 4.2 P9：体验打磨

| 功能 | 说明 | 依赖 |
|------|------|------|
| PWA | manifest + Service Worker，离线游玩 | 无 |
| 本地排行榜 | localStorage 多条目排序 | P4 |
| 多语言（i18n） | 中/英字典切换 | 无 |
| 手柄支持 | Gamepad API 标准映射 | 无 |
| 受击方向指示器 | 被打时提示伤害来源 | P3 |
| 弹药管理 UI | 手雷补充提示 / 低弹量警告 | P3 |

### 4.3 技术债务

- **单文件体积**：当前 3363 行，P9 完成后预计 3800-4200 行，仍在可控范围。
- **区段冲突**：多 Agent 改同文件需严格串行 + re-read。
- **移动端性能回归**：新增渲染逻辑需在低画质档验证 draw call 与粒子数。
- **存档兼容**：`SAVE_KEY = "fk_save_v1"`，后续若结构变更需写迁移逻辑。
- **README 截图**：当前为 AI 概念图（hero-banner.jpg / night-combat.jpg），非真实游戏截图。P7 画质完成后可替换为真实截图。
- **P8 biome 切换**：通关时全量重建地形（genWorld + buildAllChunks），低画质档可能瞬时卡顿，需验证。

---

## 5. 下一步

P8.3 通关奖励已完成，P8 多场景/关卡系统核心功能全部落地。下一步：
1. **P8.4**：浏览器验证 + 本地 commit + push 双部署同步
2. **P9**：体验打磨（PWA / 排行榜 / i18n / 手柄 / 受击指示器）

---

## 6. 参考

- 调研报告：[fps-capability-research.md](file:///d:/code/fps-world/docs/fps-capability-research.md)
- 协作规则：[AGENTS.md](file:///d:/code/fps-world/AGENTS.md)
- 项目代码：[minecraft-fps.html](file:///d:/code/fps-world/minecraft-fps.html)
