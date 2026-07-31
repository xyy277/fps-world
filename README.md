<div align="center">

# 🎮 Block FPS · 方块枪战

**A single-file, zero-install, instantly-playable voxel first-person shooter.**
Supports PC keyboard/mouse + mobile touch · Built with Three.js

[![Play on GitHub Pages](https://img.shields.io/badge/Play-GitHub%20Pages-181717?style=for-the-badge&logo=github)](https://xyy277.github.io/fps-world/minecraft-fps.html)
[![Play on Cloudflare](https://img.shields.io/badge/Play-Cloudflare%20Pages-F38020?style=for-the-badge&logo=cloudflare)](https://fps-world.pages.dev/minecraft-fps.html)
[![View on GitHub](https://img.shields.io/badge/View-GitHub-181717?style=for-the-badge&logo=github)](https://github.com/xyy277/fps-world)
[![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)](#-license)
[![Single File](https://img.shields.io/badge/single%20file-HTML-22c55e?style=for-the-badge)](minecraft-fps.html)
[![Lines of Code](https://img.shields.io/badge/lines-2600+-orange?style=for-the-badge)](minecraft-fps.html)

**👆 Click any badge above to play instantly — no download, no install, no login.**

[简体中文](README.zh-CN.md) · **English**

</div>

---

## 📸 Screenshots

<div align="center">

![Block FPS Hero Banner](docs/screenshots/hero-banner.jpg)

*Daytime voxel battlefield — trees, blocks, and approaching enemies*

![Night Combat Scene](docs/screenshots/night-combat.jpg)

*Night combat — rain, torchlight, sniper scope, damage numbers*

</div>

---

## 📑 Table of Contents

- [✨ Features](#-features)
- [🎮 Controls](#-controls)
- [🚀 Play Now](#-play-now)
- [💻 Run Locally](#-run-locally)
- [🛠 Tech Stack](#-tech-stack)
- [📂 Project Structure](#-project-structure)
- [🤝 Contributing](#-contributing)
- [🗺 Roadmap](#-roadmap)
- [📜 License](#-license)

---

## ✨ Features

> Minecraft-style × First-person shooter × Wave survival, all in **one HTML file**.

### World & Rendering
- 🌍 **Procedural voxel world** — 64×64×24 terrain with trees, rocks, and cover, regenerated every game
- 🌗 **Day-night cycle** — Wide visibility by day, frenzied zombies by night; atmosphere and difficulty shift together
- 🌧 **Dynamic weather** — Rain/snow particle system tied to day-night, randomly switches (clear/rain/snow)
- 🎨 **Zero asset dependencies** — All textures procedurally generated via Canvas 2D, all audio synthesized via Web Audio (no image/audio files)
- ✨ **Bloom post-processing** — ACES Filmic tone mapping on high quality for a cinematic look (toggleable)

### Combat & Weapons
- 🔫 **Three weapons** — Rifle (auto) / Shotgun (close burst) / Sniper (high-power scope), switch via mouse wheel or keys
- 💥 **Recoil & dynamic bloom** — Spread grows with sustained fire, recovers on stop; reload animation with gun dip
- 💣 **Grenades & TNT** — Throwable grenades with parabolic physics; place TNT and chain-detonate for crowd clear
- 🗡 **Melee attack** — Fan-shaped hit detection with cooldown for close-quarters
- 🎯 **Headshot = 2× damage** — Golden hitmarker on head hits, double damage
- ❤️ **Drop system** — Enemies drop hearts (heal) and ammo, rewarding aggression

### Enemies & AI
- 🧟 **Wave survival** — Zombies and Creepers attack in waves, escalating in fury; clearing a wave heals +25
- 🧠 **FSM enemy AI** — State machine (chase/attack/flee/wander) with A* pathfinding (10×10 grid, 500-iter cap)
- 🛡 **Cover & prediction** — Enemies use cover and predict player movement

### Progression & Save (RPG-lite)
- 💾 **Persistent save** — localStorage stores best score, best wave, total kills, total games, total headshots, best streak
- 🏆 **12 achievements** — In-game real-time detection + toast notifications + achievement wall (First Kill → Legend)
- 📈 **XP & leveling** — Kill +10xp, clear wave +20xp; level up grants skill points
- ⬆ **Upgrade tree** — 4 attributes × 5 levels, all actually affect gameplay:
  - Damage +10%/lvl (bullets & melee)
  - Max HP +15/lvl (replaces hardcoded 100)
  - Reload speed -10%/lvl
  - Move speed +8%/lvl

### Audio
- 🎵 **Procedural BGM** — Three looping tracks (menu/battle/game-over) synthesized via Oscillator+GainNode, 8-bit chiptune aesthetic
- 🔊 **Full SFX** — Gunfire, explosions, footsteps, reloads, hits, UI clicks, all synthesized
- 🔇 **Default muted** — First visit is silent (avoids startling); toggle in settings, remembered across sessions

### UI & Feedback
- 🎯 **Dynamic crosshair** — Expands with bloom
- 💬 **Damage numbers** — DOM-pooled, 3D→2D projected, float & fade; gold for headshots, red for crits
- 📋 **Killfeed** — Last 5 kills, auto-fade
- 🗺 **Minimap** — Canvas 2D, refreshed every 3 frames, shows player view cone/enemies/drops
- 📊 **Stats board** — End-game table with weapon distribution, headshots, best streak
- ⚙ **Settings panel** — Quality / volume / sensitivity + 5 toggles (mute/BGM/weather/textures/bloom), all remembered

### Controls & Platforms
- 🖥 **PC keyboard & mouse** — Full key mapping + pointer lock + mouse wheel weapon switch
- 📱 **Mobile native touch** — Fixed D-pad + sprint toggle + swipe look + action buttons (fire/jump/place/reload/weapon/scope/grenade/melee)
- 🎮 **First-time tutorial** — Operation hints shown on first game start (6s fade), with separate PC/touch versions

## 🎮 Controls

### PC (Keyboard & Mouse)

| Key | Action | Key | Action |
|-----|--------|-----|--------|
| W A S D | Move | Mouse | Look |
| Left Click | Shoot (break block / detonate TNT) | Right Click | Aim down sights (ADS, half spread) |
| Q / Wheel | Switch weapon (pistol/rifle/shotgun/sniper/rocket) | F | Sniper scope (sniper only) |
| C / Middle Click | Place block | 1 - 6 | Select block (6 = TNT) |
| R | Reload | G | Grenade |
| E | Skill: Sprint | Z | Skill: Shield |
| X | Skill: Time Slow | V | Melee |
| Shift | Sprint | Space | Jump |
| ESC | Pause | | |

### Mobile (Touch)

| Control | Action |
|---------|--------|
| ▲ ◀ ▼ ▶ | Left D-pad (multi-touch diagonal supported) |
| 跑 (Run) | Toggle sprint |
| Swipe blank screen | Turn view |
| 开火 / 跳 (Fire / Jump) | Shoot (hold for auto) / Jump |
| 放 / 弹 / 枪 / 镜 / 雷 / 刀 | Place / Reload / Switch / Scope / Grenade / Melee |
| Bottom hotbar | Select block (6 = TNT) |
| ⏸ | Pause (top-left) |

> 💡 Tip: Creepers self-destruct when close — prioritize them! TNT chain detonation is a crowd-clearing ace.

## 🚀 Play Now

Open either link in any modern browser:

| Platform | URL | Notes |
|----------|-----|-------|
| GitHub Pages | https://xyy277.github.io/fps-world/minecraft-fps.html | Synced with repo, updates on push |
| Cloudflare Pages | https://fps-world.pages.dev/minecraft-fps.html | Global CDN, faster access |

## 💻 Run Locally

No build step required — three options:

```bash
# Option 1: Double-click the file
Just open minecraft-fps.html in your browser

# Option 2: Local static server (recommended, avoids browser restrictions)
npx serve .
# or
python -m http.server 8000
```

## 🛠 Tech Stack

| Layer | Tech | Notes |
|-------|------|-------|
| Rendering | [Three.js r128](https://threejs.org/) | Loaded via CDN, no bundler |
| Language | Vanilla HTML / CSS / JavaScript | No framework, no compile step |
| Textures | Canvas 2D API | Procedurally generated pixel textures |
| Audio | Web Audio API | Procedurally synthesized SFX + BGM |
| Save | localStorage | Versioned JSON, persistent progression |
| Deployment | GitHub Pages + Cloudflare Pages | Static hosting, dual-deploy via GitHub Actions |

**Why single-file?** — The ultimate "instant play" experience: send a link to a friend and they're playing. No install, no login, no backend. The entire game (logic + rendering + textures + audio + progression) lives in **one HTML file**, ~2600 lines.

## 📂 Project Structure

```
fps-world/
├── minecraft-fps.html   # Game body (single file, ~2600 lines)
├── README.md            # This doc (English)
├── README.zh-CN.md      # Chinese README
├── AGENTS.md            # Multi-agent collaboration rules
├── docs/                # Research & progress docs
│   ├── fps-capability-research.md   # Single-page FPS capability research
│   ├── implementation-progress.md   # Implementation progress & roadmap
│   └── screenshots/                 # README showcase images
├── .github/workflows/   # CI: Cloudflare Pages auto-deploy
├── .gitignore           # Excludes .env and sensitive files
└── .env.example         # Credential field placeholder template
```

## 🤝 Contributing

Contributions welcome! Whether fixing bugs, refining gameplay, improving touch UX, or adding weapons/enemies.

1. Fork this repo
2. Create branch: `git checkout -b feat/your-feature`
3. Commit: `git commit -m "feat: add XXX"`
4. Push: `git push origin feat/your-feature`
5. Open a Pull Request

> For multi-agent / AI collaboration, read [AGENTS.md](AGENTS.md) first to understand role division and coding conventions.

## 🗺 Roadmap

**Completed (P0-P5)**
- [x] Architecture & performance guards (quality presets + object pooling)
- [x] Weapon feel (recoil + dynamic bloom + reload anim + grenades + melee)
- [x] Enemy AI (FSM + A* pathfinding + cover & prediction)
- [x] Combat UI (damage numbers + minimap + killfeed + stats board + settings)
- [x] Save & progression (localStorage + 12 achievements + upgrade tree)
- [x] Immersion (procedural BGM + weather + bloom + tutorial + 5 toggles)

**Planned (P6-P7)**
- [ ] More weapons (pistol, rocket launcher)
- [ ] More enemy types (skeleton archer, spider)
- [ ] Boss fights
- [ ] Active skills (sprint / shield / time slow)
- [ ] Local leaderboard
- [ ] PWA offline + i18n + gamepad support
- [ ] More terrain biomes

> See [docs/](docs/) for detailed research and progress.

## 📜 License

MIT License — free to use, modify, distribute. Dropping a ⭐ Star is the best encouragement!

---

<div align="center">

**If you enjoyed the game, give it a ⭐ Star!**

Made with ❤️ and Three.js

</div>
