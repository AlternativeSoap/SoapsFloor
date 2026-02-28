# GUI Menus

SoapsFloor includes a fully config-driven GUI menu system. Every menu, item, action, sound, and permission is defined in `gui.yml` and can be customized without touching code.

To open the main menu:

```
/sf menu
```

---

## Architecture

The GUI system is built on two centralized utilities:

- **GuiUtils** — Creates items from config, populates inventories, handles permissions, sounds, placeholders, and toggle-state rendering.
- **ActionHandler** — Parses and executes bracket-format action strings (e.g. `[open_menu] room_browser`).

All menus read their layout, items, and actions directly from `gui.yml`. Adding, removing, or rearranging items only requires editing the config file.

---

## Global Settings

The `settings` block at the top of `gui.yml` controls system-wide GUI behavior:

```yaml
settings:
  enabled: true
  filler-material: GRAY_STAINED_GLASS_PANE
  filler-name: " "
  open-sound: BLOCK_CHEST_OPEN
  open-sound-volume: 0.7
  open-sound-pitch: 1.2
  click-sound: UI_BUTTON_CLICK
  click-sound-volume: 0.5
  click-sound-pitch: 1.0
```

| Option | Default | Description |
|--------|---------|-------------|
| `enabled` | `true` | Master toggle for all GUI panels. |
| `filler-material` | `GRAY_STAINED_GLASS_PANE` | Material used to fill empty inventory slots. |
| `filler-name` | `" "` | Display name for filler items (blank space hides it). |
| `open-sound` | `BLOCK_CHEST_OPEN` | Sound played when any GUI opens. Set to `NONE` to disable. |
| `open-sound-volume` | `0.7` | Volume of the open sound. |
| `open-sound-pitch` | `1.2` | Pitch of the open sound. |
| `click-sound` | `UI_BUTTON_CLICK` | Sound played on every item click. Set to `NONE` to disable. |
| `click-sound-volume` | `0.5` | Volume of the click sound. |
| `click-sound-pitch` | `1.0` | Pitch of the click sound. |

---

## Action System

All item actions use a **bracket format**. The action is defined per item in `gui.yml`:

```yaml
my-button:
  slot: 11
  material: EMERALD
  name: "<green>Click Me</green>"
  action: "[open_menu] room_browser"
```

### Action Reference

| Action | Argument | Description |
|--------|----------|-------------|
| `[close]` | — | Close the GUI |
| `[open_menu]` | Menu ID | Open another menu |
| `[command]` | Command string | Run a command as the player (supports placeholders) |
| `[prev_page]` | — | Go to previous page (paginated GUIs) |
| `[next_page]` | — | Go to next page (paginated GUIs) |
| `[refresh]` | — | Refresh the current GUI |
| `[join_random]` | — | Join a random available room |
| `[leave_session]` | — | Leave the current room session |
| `[help]` | — | Show the help/command list in chat |
| `[toggle]` | `feedback`, `actionbar`, or `preview` | Toggle a player/editor setting |
| `[reload]` | — | Reload plugin configuration |
| `[debug]` | — | Show debug info |
| `[tab]` | `time` or `kills` | Switch leaderboard tab |
| `[none]` | — | No action (decorative item) |

### Menu IDs for `[open_menu]`

| ID | Opens |
|----|-------|
| `main_hub` | Main Hub |
| `room_browser` | Room Browser |
| `stats` | Player Stats |
| `settings` | Player Settings |
| `admin` | Admin Control |
| `leaderboards` | Leaderboard Room Selector |
| `leaderboard_view` | Leaderboard View |
| `schematic_browser` | Schematic Browser |

---

## Per-Item Permissions

Any item can require a permission to be shown and clickable:

```yaml
admin_control:
  slot: 29
  material: REDSTONE_TORCH
  name: "<red>Admin Control</red>"
  permission: soapsfloor.admin.gui
  action: "[open_menu] admin"
```

If the player lacks the permission, the item is hidden from the GUI entirely.

---

## Toggle / Active States

Items that represent toggleable settings can define alternate materials, names, and lore for their active state:

```yaml
toggle-feedback:
  slot: 11
  material: COMPARATOR
  material-active: REDSTONE_TORCH
  name: "<gray>Feedback Mode</gray>"
  name-active: "<green>Feedback Mode (Active)</green>"
  lore:
    - "<gray>Current: <white>{feedback_mode}"
  lore-active:
    - "<green>Currently active</green>"
  action: "[toggle] feedback"
```

When the toggle is active, the `material-active`, `name-active`, and `lore-active` fields are used instead of their base counterparts.

---

## Menus

### Main Hub

The central menu. Access everything from here.

| Item | Action | Permission |
|------|--------|------------|
| Leaderboards | `[open_menu] leaderboards` | — |
| Your Stats | `[open_menu] stats` | — |
| Commands | `[help]` | — |
| Quick Join | `[join_random]` | — |
| Room Browser | `[open_menu] room_browser` | — |
| Session Status | `[none]` (info only) | — |
| Admin Control | `[open_menu] admin` | `soapsfloor.admin.gui` |
| Leave Session | `[leave_session]` | — |
| Settings | `[open_menu] settings` | `soapsfloor.admin.gui` |
| Close | `[close]` | — |

---

### Room Browser

A paginated list of all available rooms. Each room shows:

- Room name
- Number of floors
- Current players / max players
- Room status (waiting, in progress, celebrating, etc.)
- Your best time for that room

Click any room to join it. Navigation buttons at the bottom:

| Item | Action |
|------|--------|
| Previous | `[prev_page]` |
| Refresh | `[refresh]` |
| Back | `[open_menu] main_hub` |
| Next | `[next_page]` |

---

### Player Stats

Shows your personal statistics:

| Stat | Description |
|------|-------------|
| Monsters Killed | Total kills across all runs |
| Games Completed | Number of successful dungeon completions |
| Best Time (Current Room) | Your fastest completion time for the room you're currently in |
| Best Time (Overall) | Your fastest time across all rooms, and which room it was |
| Rooms Tracked | Number of rooms where you have a recorded best time |

Navigation: Back (`[open_menu] main_hub`) and Close (`[close]`).

---

### Player Settings

Personal toggles that affect your experience:

| Setting | Action | Description |
|---------|--------|-------------|
| Feedback Mode | `[toggle] feedback` | Toggle between chat messages and action bar for editor feedback |
| Actionbar Hints | `[toggle] actionbar` | Toggle action bar hints on/off during wand editing |
| Floor Preview | `[toggle] preview` | Toggle ghost block previews on/off during wand editing |

Navigation: Back (`[open_menu] main_hub`) and Close (`[close]`).

---

### Admin Control

Available to players with `soapsfloor.admin.gui`.

| Action | Bracket Action | Permission |
|--------|----------------|------------|
| Reload Config | `[reload]` | `soapsfloor.admin.gui` |
| Debug Info | `[debug]` | `soapsfloor.admin.gui` |
| Room Browser | `[open_menu] room_browser` | — |
| Main Hub | `[open_menu] main_hub` | — |
| Close | `[close]` | — |

---

### Leaderboard — Room Selector

A paginated list of rooms. Click a room to view its leaderboard.

Each room entry shows the room name and floor count. Navigation:

| Item | Action |
|------|--------|
| Previous | `[prev_page]` |
| Back | `[open_menu] main_hub` |
| Close | `[close]` |
| Next | `[next_page]` |

---

### Leaderboard — View

After selecting a room, you see its leaderboard with two tabs:

| Tab | Action | Ranks By |
|-----|--------|----------|
| Best Time | `[tab] time` | Fastest completion time |
| Best Kills | `[tab] kills` | Most kills in a single run |

Each entry shows the rank, player name, and value. Navigation: Back (`[open_menu] leaderboards`) and Close (`[close]`).

---

### Schematic Browser

Used during room editing or as a standalone tool via `/sf wand schematics`. Shows all available `.schem` files in `plugins/SoapsFloor/schematics/`.

Each schematic displays:
- **Name** — The schematic file name
- **Size** — Dimensions in blocks (e.g., `Size: 12x8x12 blocks`)

Navigation: Previous (`[prev_page]`), Next (`[next_page]`), Close (`[close]`).

#### Editor Mode (during `/sf wand create` or `/sf wand edit`)

Click a schematic to select it for a floor. After selecting, a floor count selector appears where you can choose how many floors to create with that schematic.

#### Standalone Mode (`/sf wand schematics`)

Click a schematic to enter **preview mode**:

1. The GUI closes and a ghost preview of the schematic appears in-world
2. Ghost blocks are semi-transparent (scaled 0.85) with a glowing outline and particle border
3. The preview follows your crosshair direction
4. **Scroll wheel** — Adjusts the distance of the preview from you (range: 3–50 blocks)
5. The action bar shows the current distance and instructions
6. Type **`done`** in chat to paste the schematic at the preview location
7. Type **`cancel`** in chat to abort without pasting
8. Type **`undo`** in chat after pasting to revert the paste and restore original blocks

This is useful for placing starter rooms or any schematic without needing WorldEdit/FAWE.

---

## Customizing Menus

All menus are configured in `gui.yml`. You can change:

- **Menu size** (rows of 9 slots)
- **Title** (MiniMessage formatting)
- **Item positions** (slot numbers)
- **Item materials** (any Minecraft material)
- **Item names and lore** (MiniMessage formatting)
- **Custom model data** (for resource packs)
- **Actions** (bracket-format action strings)
- **Permissions** (per-item permission nodes)
- **Toggle states** (`material-active`, `name-active`, `lore-active`)
- **Global sounds** (open and click sounds in the `settings` block)

### Multi-Slot Items

Any item can be placed in multiple slots at once:

```yaml
border:
  slot: "0,1,2,3,4,5,6,7,8"
  material: GRAY_STAINED_GLASS_PANE
  name: " "
```

### Available Placeholders

Placeholders in item names and lore are automatically replaced:

| Placeholder | Where | Value |
|-------------|-------|-------|
| `{player}` | Main Hub | Player's name |
| `{in_session}` | Main Hub | Yes/No |
| `{current_room}` | Main Hub | Current room name or "None" |
| `{rooms_available}` | Main Hub | Number of available rooms |
| `{total_kills}` | Player Stats | Total kill count |
| `{games_completed}` | Player Stats | Games completed count |
| `{best_time_current_room}` | Player Stats | Best time for current room |
| `{best_time_overall}` | Player Stats | Best time across all rooms |
| `{best_room_name}` | Player Stats | Room name for best overall time |
| `{rooms_with_best}` | Player Stats | Rooms with best times |
| `{room_id}` | Room Browser / Leaderboard | Room name |
| `{floors}` | Room Browser / Leaderboard | Floor count |
| `{players}` | Room Browser | Current player count |
| `{max_players}` | Room Browser | Max player count |
| `{status}` | Room Browser | Room status |
| `{best_time}` | Room Browser | Player's best time |
| `{room}` | Leaderboard View | Room name |
| `{tab}` | Leaderboard View | Current tab name |
| `{rank}` | Leaderboard View | Player rank |
| `{value}` | Leaderboard View | Time or kill value |
| `{schematic}` | Schematic Browser | Schematic name |
| `{size}` | Schematic Browser | Schematic dimensions (WxHxL) |
| `{page}` | Paginated menus | Current page number |
| `{feedback_mode}` | Settings | Current feedback mode |
| `{actionbar_state}` | Settings | Actionbar hints state |
| `{preview_state}` | Settings | Preview state |

### MiniMessage Formatting

All text fields support MiniMessage formatting:

```yaml
name: "<gradient:#f59e0b:#fbbf24><bold>My Item</bold></gradient>"
lore:
  - ""
  - "<gray>Some description text"
  - "<gold>Click to do something</gold>"
```

Reference: [MiniMessage Docs](https://docs.advntr.dev/minimessage/format.html)

---

## Disabling the GUI

You can disable the GUI system in two ways:

**Via `config.yml`:**
```yaml
gui:
  enabled: false
```

**Via `gui.yml` settings block:**
```yaml
settings:
  enabled: false
```

All features remain accessible through commands when the GUI is disabled.

---

**Previous:** [Falling Hazard](Falling-Hazard.md) | **Next:** [Commands & Permissions](Commands-and-Permissions.md)
