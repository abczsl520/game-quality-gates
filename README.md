# 🎮 Game Quality Gates

> **An [OpenClaw](https://github.com/openclaw/openclaw) Agent Skill** — Mandatory quality standards for H5/Canvas/WebGL game projects.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-blue)](https://github.com/openclaw/openclaw)

## What is this?

A battle-tested set of **12 universal rules + engine-specific guides** that prevent the most common game bugs before they ship. Born from fixing **70+ real bugs** in production H5 games and validated against industry best practices.

## The Core Insight

> **Bugs don't come from individual features — they come from cross-state interactions.**

Every feature works fine alone. They break in combination:
- Slow powerup + paddle collision = speed conflict
- Multi-ball + main ball death = orphan sub-balls
- Power-up falling + death timing = ghost objects
- Game over + buff timers = lifecycle leaks

## 📋 The 12 Universal Rules

| # | Rule | What it prevents |
|---|------|-----------------|
| 1 | 🔄 Single Cleanup Entry Point | "Fixed in A, forgot in B" bugs |
| 2 | ⚡ Respect Active Buffs | Buff/debuff being silently overwritten |
| 3 | 📦 Cache Before Destroy | Reading dead object properties |
| 4 | ⏰ Timers Follow Lifecycle | Phantom timers firing after game over |
| 5 | 🖥️ Frame-Rate Independent Logic | 30fps device = half speed |
| 6 | 🚪 Scene Transition = Full Cleanup | Memory leaks between levels |
| 7 | 🔊 Audio Lifecycle | iOS silent, background tab still playing |
| 8 | 👆 Input Safety | Double-buy, rapid-fire exploits |
| 9 | 💾 Save State Persistence | Lost progress, broken saves after update |
| 10 | 🌐 Network Fault Tolerance | Game freezes on bad network |
| 11 | 📦 Asset Loading Strategy | White screen, missing textures |
| 12 | 🛡️ Anti-Cheat Baseline | Score injection, payment bypass |

## 🎯 Engine-Specific Guides

### Phaser (Arcade Physics)
- Multi-touch pointer ID tracking
- Physics group cross-level cleanup
- OVERLAP_BIAS tuning (recommended: 3-4)
- `physics.pause()` vs `time.delayedCall` independence

### Three.js (WebGL/3D)
- Dispose trio: geometry + material + texture
- GLB compression pipeline (14MB → 800KB)
- Animation crossfade state machine
- `gltf-transform prune` Skin deletion pitfall

### Anti-Cheat Patterns
- One-time raid tokens
- Server-side duration validation
- Operation sequence enforcement

## 🚀 Installation

### For OpenClaw users

Copy to your skills directory:

```bash
git clone https://github.com/abczsl520/game-quality-gates.git ~/.openclaw/skills/game-quality-gates
```

Restart OpenClaw Gateway. The skill auto-triggers when you work on game projects.

### For everyone else

Just read the docs! The knowledge is useful regardless of your AI setup:

- **[SKILL.md](SKILL.md)** — All 12 universal rules + pre-deploy checklist
- **[references/phaser.md](references/phaser.md)** — Phaser engine specifics
- **[references/threejs.md](references/threejs.md)** — Three.js engine specifics
- **[references/anti-cheat.md](references/anti-cheat.md)** — Web game anti-cheat patterns

## 📁 Structure

```
game-quality-gates/
├── SKILL.md                    # Core rules + checklists (auto-loaded)
└── references/
    ├── phaser.md               # Phaser-specific rules (loaded on demand)
    ├── threejs.md              # Three.js-specific rules (loaded on demand)
    └── anti-cheat.md           # Anti-cheat patterns (loaded on demand)
```

## 🏷️ Pre-Deploy Checklist (Quick Version)

```
🔴 Universal (every game)
  □ New objects in cleanupGameState()?
  □ New timers cancelled in cleanup?
  □ Attributes respect active buffs?
  □ Data cached before destroy?
  □ Delta time used for movement?
  □ No memory leaks across scenes?
  □ Audio pauses on background?
  □ Purchase has click-lock?
  □ Save has version + migration?
  □ Network has timeout + fallback?
  □ Load failure has degradation?
  □ Critical ops server-validated?

🟡 Mobile Extra
  □ Multi-touch tracked per finger?
  □ iOS AudioContext resumed?
  □ WeChat WebView compatible?
  □ Controls don't overlap game?
  □ Orientation change handled?
```

## 📊 Origin Data

- **Source project**: pixel-bounce (像素弹球王) — 70+ bugs fixed across 10 rounds
- **Source project**: tripo-3d-demo (柯基跑酷3D) — model compression + animation
- **Industry references**: Phaser forum best practices, Three.js dispose docs, web game anti-cheat literature (2024-2025)

## 📄 License

MIT — Use freely, attribution appreciated.
