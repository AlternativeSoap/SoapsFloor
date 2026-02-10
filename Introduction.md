# Introduction

SoapsFloor is a vertical dungeon plugin where players fall through progressively harder floors. You build the dungeon rooms using WorldEdit/FAWE schematics, the plugin stacks them vertically, and players drop down floor by floor as they clear all the mobs on each level.

---

## How It Works

The concept is simple:

1. A **room** is a dungeon. Each room has a **starter area** at the top and multiple **floors** stacked below it.
2. Players join a room and spawn in the starter area.
3. After a countdown, the floor beneath them breaks and they fall to **Floor 1**.
4. Mobs spawn on the floor. Players must kill all of them.
5. Once the floor is cleared, another countdown starts and the floor drops again.
6. This repeats until all floors are completed or the player dies.

Players who survive all floors win the dungeon and get teleported out. Their completion time, kills, and stats are tracked and saved.

---

## Key Features

**Room Building**
- Build rooms visually using a wand tool and WorldEdit/FAWE schematics
- Each floor can use a different schematic
- One schematic can span multiple floors at once
- Per-floor mob configuration (type, count, spread)
- Custom commands per floor (run any command when a floor starts)

**Gameplay**
- Solo or multiplayer (configurable player limits)
- Waiting lobby with timer before the run starts
- Countdown before each floor drop with sound effects
- Anti-cheese protections (no elytra, no ender pearls, no flying)
- Configurable death behavior (kick, spectate, or respawn)
- Floor drop particle and sound effects
- Victory rewards via custom commands

**Falling Hazard** (optional)
- A descending plane of particles that falls from the ceiling
- Players above it die instantly, players inside it take damage
- Forces players to keep moving down instead of camping

**Stats & Leaderboards**
- Per-player stats: total kills, games completed, best times
- Per-room leaderboards ranked by fastest time or most kills
- All stats persist across server restarts

**GUI Menus**
- Main hub menu with quick join, room browser, stats, settings
- Room browser with pagination
- Leaderboard viewer per room
- Admin control panel
- Player settings menu
- All fully customizable through gui.yml

**MythicMobs Support**
- Use vanilla mobs or MythicMobs on any floor
- Format: `VANILLA:ZOMBIE` or `MYTHIC:FireDemon`
- Mix and match per floor

---

## Plugin Structure

When installed, SoapsFloor creates this folder structure:

```
plugins/SoapsFloor/
  config.yml          # Main configuration
  messages.yml        # All plugin messages (MiniMessage format)
  gui.yml             # GUI menu layouts and items
  rooms/              # Saved room data (one .yml per room)
  schematics/         # WorldEdit/FAWE .schem files go here
  data/               # Player stats (one .yml per player UUID)
```

---

## Soft Dependencies

| Plugin | Required? | Used For |
|--------|-----------|----------|
| WorldEdit / FAWE | Yes | Schematic pasting for floor layouts. FAWE is recommended. |
| MythicMobs | No | Custom mob spawning on floors |

---

**Next:** [Getting Started](Getting-Started)
