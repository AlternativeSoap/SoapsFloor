# Commands & Permissions

Every command in SoapsFloor and the permission nodes that control access.

---

## Commands

All commands use the base `/sf` (alias: `/soapsfloor`).

### Player Commands

| Command | Description |
|---------|-------------|
| `/sf help` | Show all available commands |
| `/sf menu` | Open the main GUI menu |
| `/sf stats` | Open your statistics page |
| `/sf room <room_id>` | Join a room |
| `/sf room list` | List all available rooms |
| `/sf room info <room_id>` | Show details about a room |
| `/sf room leave` | Leave your current room |
| `/sf settings toggle feedback` | Toggle feedback between chat and action bar |

### Admin Commands

| Command | Description |
|---------|-------------|
| `/sf reload` | Reload all config files |
| `/sf debug` | Show debug mode status |
| `/sf wand create <room_id>` | Start creating a new room |
| `/sf wand edit <room_id>` | Edit an existing room |
| `/sf wand finish` | Save and exit editor mode |
| `/sf wand cancel` | Cancel editing without saving |
| `/sf wand status` | Show current editor session info |
| `/sf wand list` | List all saved rooms |
| `/sf wand floors` | Show floor configuration for current session |
| `/sf wand remove <room_id>` | Delete a room |
| `/sf wand settings` | Show editor settings commands |
| `/sf wand settings toggle feedback` | Toggle editor feedback to chat or action bar |
| `/sf wand settings toggle actionbar` | Toggle action bar hints |
| `/sf wand settings toggle preview` | Toggle floor preview ghost blocks |
| `/sf room delete <room_id>` | Delete a room |

---

## Permissions

### Wildcard

| Permission | Default | Description |
|-----------|---------|-------------|
| `soapsfloor.*` | OP | All SoapsFloor permissions |

### Admin Permissions

| Permission | Default | Description |
|-----------|---------|-------------|
| `soapsfloor.admin` | OP | All admin permissions |
| `soapsfloor.admin.reload` | OP | Reload configuration |
| `soapsfloor.admin.wand` | OP | All wand/editor commands |
| `soapsfloor.admin.wand.create` | OP | Create new rooms |
| `soapsfloor.admin.wand.edit` | OP | Edit existing rooms |
| `soapsfloor.admin.wand.remove` | OP | Remove rooms |
| `soapsfloor.admin.wand.settings` | OP | Editor settings |
| `soapsfloor.admin.room.delete` | OP | Delete rooms |
| `soapsfloor.admin.debug` | OP | Debug commands |
| `soapsfloor.admin.gui` | OP | Admin control panel in GUI |

### Player Permissions

| Permission | Default | Description |
|-----------|---------|-------------|
| `soapsfloor.player` | Everyone | All player permissions |
| `soapsfloor.player.menu` | Everyone | Open the GUI menu |
| `soapsfloor.player.stats` | Everyone | View personal stats |
| `soapsfloor.player.room.join` | Everyone | Join rooms |
| `soapsfloor.player.room.leave` | Everyone | Leave rooms |
| `soapsfloor.player.room.list` | Everyone | List available rooms |

---

## Permission Setup Examples

### Give all players access to play (default behavior)

No setup needed. All player permissions default to `true`.

### Restrict room joining to a specific rank

Using LuckPerms:

```
/lp group default permission set soapsfloor.player.room.join false
/lp group vip permission set soapsfloor.player.room.join true
```

### Give a builder access to create rooms

```
/lp group builder permission set soapsfloor.admin.wand.create true
/lp group builder permission set soapsfloor.admin.wand.edit true
```

### Give full admin access

```
/lp group admin permission set soapsfloor.admin true
```

Or simply:

```
/lp group admin permission set soapsfloor.* true
```

---

**Previous:** [GUI Menus](GUI-Menus) | **Next:** [Examples](Examples)
