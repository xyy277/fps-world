# 实施进度与后续目标

> 更新时间：2026-07-31
> 当前代码规模：3653 行（minecraft-fps.html）
> 本地领先 origin/main：7 个 commit（P6.3-P8.3 已 commit，P9.1-P9.5 待 commit）

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
| 多场景/关卡（P8） | ✅ 已完成（P8.1-P8.3 已落地并 commit，P8.4 浏览器验证待做） |
| 体验打磨（P9） | 🔄 进行中（P9.1-P9.5 已完成，P9.3 PWA 暂缓，P9.6 待提交） |
| GitHub Pages 部署 | ✅ 在线（落后本地 2 commit） |
| Cloudflare Pages 部署 | ✅ 在线（落后本地 2 commit） |
| 双部署自动同步（Actions） | ✅ 已配置 |

**阶段结论**：P0-P8 全部落地，游戏具备完整单局循环 + 长期进度 + 视听反馈 + 多武器多敌人 + Boss 战 + 主动技能 + 画质增强 + 多场景关卡 + 通关奖励。P9 体验打磨进行中（本地排行榜已完成），剩余 PWA/i18n/手柄/受击指示器为后续。

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

### P9.1：本地排行榜
- localStorage 持久化 Top 10 成绩（按 score 降序，超出 10 条截断）
- 每条记录：{ id, score, wave, kills, level, date }，id 用 Date.now() 唯一标识本局
- 局末 finalizeGameStats 自动入库；旧存档兼容（loadSave 检测 leaderboard 数组）
- 排行榜面板：Top 10 表格（排名/得分/波次/击杀/关卡/日期）
  - 前三名金/银/铜色排名标识
  - 本局成绩金色高亮（lb-self 行）
  - 空状态提示
- UI 入口：菜单 / 游戏结束 / 暂停界面均新增「🏆 排行榜」按钮
- startGame 重置 lastRunId，避免新游戏后从菜单查看误高亮上一局

### P9.2：受击方向指示器 + 弹药管理 UI
- **受击方向指示器**：玩家被攻击时，屏幕中央显示红色三角箭头指向伤害来源方向
  - damagePlayer(d, srcX, srcZ) 增加可选来源坐标参数
  - 用相机前向向量与来源向量计算相对角度（0=正前方，正=右侧，负=左侧）
  - CSS clip-path 三角形 + transform: rotate 指向来源，1s 淡出
  - 所有 7 处敌人/爆炸伤害调用点均传入来源坐标（跌落伤害无来源，不显示指示器）
- **低弹量警告**：当前弹匣 ≤ 总容量 25% 且非空时，弹药数字红色闪烁
- **手雷耗尽提示**：手雷为 0 时，💣 数字红色闪烁
- startGame 清理残留指示器，避免重开后残留

### P9.4：轻量 i18n（中/英切换）
- **策略**：关键静态 UI 节点加 `data-i18n="key"` 属性，切换时遍历替换 textContent；动态文本（伤害数字/banner/killfeed）不翻译
- **字典**：约 30 个 key，覆盖菜单/暂停/游戏结束/面板标题/按钮/昼夜标签
- **切换**：菜单新增「🌐 中文 / English」按钮，点击中英互切
- **持久化**：save.lang 字段（"zh"/"en"），loadSave 兼容旧存档默认 "zh"
- **applyI18n()**：启动时按存档语言应用；切换时刷新所有 [data-i18n] 节点 + padToggle 按钮

### P9.5：手柄支持（标准 FPS 映射）
- **轮询**：pollGamepad() 在主循环 state==="playing" 时调用，navigator.getGamepads() 读取
- **摇杆**：左摇杆→移动（模拟量叠加到 ix/iz，死区 0.15），右摇杆→视角（死区 0.12，灵敏度与鼠标体系一致）
- **按钮映射**（standard mapping）：
  - A=跳跃 / X=换弹 / Y=近战 / B=暂停（边沿触发）
  - RT=射击（保持）/ LT=瞄准（保持）
  - RB/LB/Back=切武器 / L3=手雷 / R3=建造 / Start=暂停
- **边沿检测**：padPrev 记录上一帧按钮状态，上升沿触发一次性动作
- **开关**：菜单新增「🎮 手柄：开/关」按钮，持久化到 save.padEnabled
- **兼容**：手柄输入叠加到现有 keys/dpad 体系，不破坏键盘+触屏双输入

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

### 4.1 P9 剩余：体验打磨

| 编号 | 功能 | 说明 | 优先级 |
|------|------|------|--------|
| P9.2 | ~~受击方向指示器 + 弹药管理 UI~~ | ✅ 已完成（见上文 P9.2 详表） | � 中 |
| P9.3 | ~~PWA 离线游玩~~ | ⏸️ 暂缓——PWA 需 manifest.json + sw.js 独立文件，违反「单 HTML 文件」铁律，待所有者决定是否放宽 | 🟡 中 |
| P9.4 | ~~多语言（i18n）~~ | ✅ 已完成（见上文 P9.4 详表） | 🟢 低 |
| P9.5 | ~~手柄支持~~ | ✅ 已完成（见上文 P9.5 详表） | 🟢 低 |
| P9.6 | 浏览器验证 + commit + push | 人工回归 P9 全部内容，确认无报错后提交并双部署 | 🔴 高 |

### 4.2 P10 构想：多人联机 PVE（新阶段）

**目标**：本地 ws 服务 + 公网穿透，支持创建房间多人合作 PVE（非 PVP，延迟不敏感，乐趣优先）

| 模块 | 技术选型 | 说明 |
|------|----------|------|
| 后端 | Python FastAPI + websockets（或 Node.js + ws） | 用户熟悉 FastAPI，复用现有技能栈 |
| 穿透 | Cloudflare Tunnel（免费/稳定/已有账号） | 替代 ngrok，无需付费 |
| 协议 | JSON over WebSocket | 简单优先，后续可换二进制优化带宽 |
| 架构 | 主机权威（host-authoritative） | 房主跑敌人模拟，客户端发输入 + 收状态，避免状态冲突 |
| 同步内容 | 玩家位置/朝向/射击事件/敌人状态/掉落 | PVE 下 100-200ms 延迟可接受 |
| 房间管理 | 房间号 + 房主 + 最多 4 人 | 简易匹配，不做随机匹配 |

**核心玩法设想**：
- 合作打 Boss：多人分工（坦克/输出/治疗）
- 共享波次：所有人共享波次进度，分摊防守压力
- 复活机制：倒地后队友可救援，全灭才 Game Over
- 独立奖励：每人独立获得通关奖励，互不影响

**工作量评估**：大（新后端 + 协议设计 + 状态同步 + UI 房间系统），建议作为独立大阶段推进。

**铁律影响**：
- ❌ 破坏「无后端」约束（P10 明确引入后端，需所有者确认）
- ❌ 破坏「单 HTML 文件」约束（需引入 ws 客户端逻辑，但可内联到 HTML）
- ✅ 不破坏「零依赖安装」约束（CDN 加载 Three.js 不变，ws 是浏览器原生 API）

> P10 为开放式新阶段，启动前需所有者明确确认放宽「无后端」约束。

### 4.3 技术债务

- **单文件体积**：当前 3653 行，P9 完成后预计 3800-4200 行，仍在可控范围。
- **区段冲突**：多 Agent 改同文件需严格串行 + re-read。
- **移动端性能回归**：新增渲染逻辑需在低画质档验证 draw call 与粒子数。
- **存档兼容**：`SAVE_KEY = "fk_save_v1"`，后续若结构变更需写迁移逻辑。
- **README 截图**：当前为 AI 概念图（hero-banner.jpg / night-combat.jpg），非真实游戏截图。P7 画质完成后可替换为真实截图。
- **P8 biome 切换**：通关时全量重建地形（genWorld + buildAllChunks），低画质档可能瞬时卡顿，需验证。

---

## 5. 下一步

P9.1-P9.5 全部完成（P9.3 PWA 因违反单文件铁律暂缓）。下一步：
1. **P9.6**：浏览器验证 + commit + push 双部署同步（提交 P9.1-P9.5）
2. **P10**：多人联机 PVE（需所有者确认放宽「无后端」约束后启动）

---

## 6. 参考

- 调研报告：[fps-capability-research.md](file:///d:/code/fps-world/docs/fps-capability-research.md)
- 协作规则：[AGENTS.md](file:///d:/code/fps-world/AGENTS.md)
- 项目代码：[minecraft-fps.html](file:///d:/code/fps-world/minecraft-fps.html)
