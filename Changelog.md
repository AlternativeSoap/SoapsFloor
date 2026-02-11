# Changelog

All notable changes to SoapsFloor.

---

## v1.1.0 - Schematic Browser & Preview

**Schematic Browser Standalone Mode**
- New `/sf wand schematics` command to browse and paste schematics without an active wand session
- Schematic browser now shows block dimensions (Size: WxHxL) on each schematic item
- Permission: `soapsfloor.admin.wand.schematics`

**Schematic Preview System**
- Click a schematic in standalone mode to enter live preview mode
- Ghost/holographic BlockDisplay preview follows your crosshair direction
- Semi-transparent blocks (0.85 scale) with glowing outline and particle border
- Scroll wheel adjusts preview distance (range: 3–50 blocks)
- Action bar shows current distance and instructions
- Type `done` in chat to paste, `cancel` to abort

**Undo Paste**
- After pasting a schematic, type `undo` in chat to revert and restore original blocks
- Supports one level of undo per paste operation

---

## v1.0.0 - Initial Release

The first public release of SoapsFloor.

**Room System**
- Create rooms with the wand tool and WorldEdit/FAWE schematics
- Edit existing rooms at any time
- Per-room settings that override global defaults
- Rooms save as individual YAML files

**Gameplay**
- Vertical dungeon with floor-drop mechanic
- Solo and multiplayer support (up to configurable max)
- Waiting lobby with timer before runs
- Countdown before floor drops with sounds and titles
- Floor protection (no block break/place during runs)
- Victory screen with completion stats
- Configurable death behavior (kick, spectate, or respawn)
- Reward commands on victory with placeholders

**Mob Spawning**
- Vanilla mob support with per-floor configuration
- MythicMobs integration for custom mobs
- Adjustable min/max mob count per floor
- Spread radius to prevent mob stacking
- Mob counter display (action bar, chat, or boss bar)

**Falling Hazard**
- Optional descending particle plane
- Configurable speed, damage, and particle appearance
- Resets on each new floor

**Anti-Cheese**
- Elytra disabled in rooms
- Ender pearl blocking
- Flight prevention
- Configurable fall damage multiplier

**Editor Mode**
- Full wand-based room creation with guided steps
- Hotbar tools for gap, player count, countdown, and mob adjustment
- Floor preview system with ghost blocks
- Built-in how-to guide book
- Custom commands per floor
- Schematic browser GUI
- Inventory and gamemode saved and restored on exit

**GUI Menus**
- Main hub with quick join, room browser, stats, and settings
- Paginated room browser
- Player statistics viewer
- Per-room leaderboards (best time, most kills)
- Player settings toggles
- Admin control panel
- All fully customizable through gui.yml with MiniMessage support

**Stats & Leaderboards**
- Per-player persistent stats (kills, completions, best times)
- Per-room leaderboards ranked by time and kills
- Stats saved to individual player files

**Configuration**
- Full config.yml with documented options
- Customizable messages via messages.yml with MiniMessage
- GUI layouts via gui.yml
- Per-room settings override

**Server Compatibility**
- Paper 1.21+
- Java 21
- WorldEdit / FAWE integration (FAWE recommended)
- MythicMobs integration (optional)
