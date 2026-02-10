# GUI Menus

SoapsFloor includes a full GUI menu system. All menus are customizable through `gui.yml`.

To open the main menu:

```
/sf menu
```

---

## Main Hub

The central menu. Access everything from here.

| Item | Action |
|------|--------|
| Leaderboards | Opens the leaderboard room selector |
| Your Stats | Opens your personal stats page |
| Commands | Shows the help/command list in chat |
| Quick Join | Joins a random available room instantly |
| Room Browser | Browse and pick a room to join |
| Session Status | Shows your current session info (room, status) |
| Admin Control | Opens the admin panel (requires `soapsfloor.admin.gui`) |
| Leave Session | Leaves your current room session |
| Settings | Opens player settings |
| Close | Closes the menu |

---

## Room Browser

A paginated list of all available rooms. Each room shows:

- Room name
- Number of floors
- Current players / max players
- Room status (waiting, in progress, etc.)
- Your best time for that room

Click any room to join it. Use the arrows at the bottom to navigate pages.

---

## Player Stats

Shows your personal statistics:

| Stat | Description |
|------|-------------|
| Monsters Killed | Total kills across all runs |
| Games Completed | Number of successful dungeon completions |
| Best Time (Current Room) | Your fastest completion time for the room you're currently in |
| Rooms Tracked | Number of rooms where you have a recorded best time |

---

## Player Settings

Personal toggles that affect your experience:

| Setting | Description |
|---------|-------------|
| Feedback Mode | Toggle between chat messages and action bar for editor feedback |
| Actionbar Hints | Toggle action bar hints on/off during wand editing |
| Floor Preview | Toggle ghost block previews on/off during wand editing |

---

## Admin Control

Available to players with `soapsfloor.admin.gui`.

| Action | Description |
|--------|-------------|
| Reload Config | Reloads all config files |
| Debug Info | Shows debug mode status |
| Room Browser | Opens the room browser |
| Main Hub | Returns to the main menu |

---

## Leaderboard - Room Selector

A paginated list of rooms. Click a room to view its leaderboard.

Each room entry shows the room name and floor count.

---

## Leaderboard - View

After selecting a room, you see its leaderboard with two tabs:

| Tab | Ranks By |
|-----|----------|
| Best Time | Fastest completion time |
| Best Kills | Most kills in a single run |

Each entry shows the rank, player name, and value.

---

## Schematic Browser

Used during room editing. Shows all available `.schem` files in `plugins/SoapsFloor/schematics/`.

Click a schematic to select it for a floor. After selecting, a floor count selector appears where you can choose how many floors to create with that schematic.

---

## Customizing Menus

All menus are configured in `gui.yml`. You can change:

- **Menu size** (rows of 9 slots)
- **Title** (MiniMessage formatting)
- **Item positions** (slot numbers)
- **Item materials** (any Minecraft material)
- **Item names and lore** (MiniMessage formatting)
- **Custom model data** (for resource packs)

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
| `{rooms_with_best}` | Player Stats | Rooms with best times |
| `{room_id}` | Room Browser / Leaderboard | Room name |
| `{floors}` | Room Browser / Leaderboard | Floor count |
| `{players}` | Room Browser | Current player count |
| `{max_players}` | Room Browser | Max player count |
| `{status}` | Room Browser | Room status |
| `{best_time}` | Room Browser | Player's best time |
| `{feedback_mode}` | Settings | Current feedback mode |
| `{actionbar_state}` | Settings | Actionbar hints state |
| `{preview_state}` | Settings | Preview state |
| `{rank}` | Leaderboard View | Player rank |
| `{value}` | Leaderboard View | Time or kill value |

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

If you prefer commands only:

```yaml
# config.yml
gui:
  enabled: false
```

All features remain accessible through commands.

---

**Previous:** [Falling Hazard](Falling-Hazard) | **Next:** [Commands & Permissions](Commands-and-Permissions)
