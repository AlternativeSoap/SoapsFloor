# Mob System

SoapsFloor supports both vanilla Minecraft mobs and MythicMobs. You can configure mob spawning globally or per floor.

---

## Global Defaults

These are set in `config.yml` and apply to any floor that doesn't have its own settings:

```yaml
mob-spawning:
  default-min-mobs: 3
  default-max-mobs: 8
  default-mob-type: VANILLA:ZOMBIE
  default-spread-radius: 3
  spawn-delay-ticks: 0
  mob-counter-display: actionbar
```

| Option | Description |
|--------|-------------|
| `default-min-mobs` | Minimum mobs per floor |
| `default-max-mobs` | Maximum mobs per floor |
| `default-mob-type` | Default mob type for all floors |
| `default-spread-radius` | Minimum distance (in blocks) between mob spawn points |
| `spawn-delay-ticks` | Ticks between each mob spawn. `0` = instant (all at once). Set to `10` for 0.5s staggered spawns. |
| `mob-counter-display` | How remaining mobs are shown: `actionbar`, `chat`, or `bossbar` |

---

## Mob Type Format

Mob types follow this format:

```
VANILLA:<entity_type>
MYTHIC:<mythicmobs_id>
```

### Vanilla Mobs

Use Minecraft entity names in uppercase:

```
VANILLA:ZOMBIE
VANILLA:SKELETON
VANILLA:SPIDER
VANILLA:CREEPER
VANILLA:BLAZE
VANILLA:WITHER_SKELETON
VANILLA:ENDERMAN
VANILLA:WITCH
VANILLA:PILLAGER
VANILLA:VINDICATOR
```

### MythicMobs

If you have MythicMobs installed, use the mob's internal ID:

```
MYTHIC:FireDemon
MYTHIC:SkeletonKing
MYTHIC:VoidWalker
```

The MythicMobs plugin must be installed and the mob ID must exist in your MythicMobs config.

---

## Per-Floor Mob Settings

You can customize mobs for individual floors while in editor mode.

### Using the Editor

1. Select a floor using the **Floor Selector** (hotbar slot 8)
2. Use the **Mob Settings** tool (hotbar slot 9):
   - **Right-click:** Set mob type (type in chat: `vanilla:zombie` or `mythicmobs:FireDemon`)
   - **Left-click:** Adjust min/max mob count
   - **Shift-click:** Larger increments

### How It Works

Each floor stores its own mob settings independently:

- `minMobs` - Minimum mobs for this floor (`-1` = use global default)
- `maxMobs` - Maximum mobs for this floor (`-1` = use global default)
- `mobType` - Mob type for this floor (`null` = use global default)
- `spreadRadius` - Spacing between spawns

When a floor starts, the plugin:
1. Checks if the floor has custom mob settings
2. Falls back to room-level defaults
3. Falls back to global config defaults
4. Picks a random count between min and max
5. Spawns mobs spread across the floor's bounding box

---

## Multiple Mob Types Per Floor

Each floor can have multiple mob types configured. During room creation:

1. Select a floor using the **Floor Selector** (hotbar slot 8)
2. Use the **Mob Settings** tool (hotbar slot 9)
3. **Right-click** to open mob type selection
4. Type a mob in chat (e.g., `vanilla:skeleton`)
5. Right-click again to add another mob type to the same floor

When the floor starts, the plugin picks from all configured mob types for that floor. Each mob that spawns is randomly selected from the floor's mob list.

### Example

A floor configured with:
- `VANILLA:ZOMBIE`
- `VANILLA:SKELETON`
- `MYTHIC:FireDemon`

Will spawn a mix of all three mob types, randomly distributed across the mob count.

---

## Mob Counter Display

While fighting mobs, players see how many are left. Configure the display method:

| Mode | Where It Shows |
|------|---------------|
| `actionbar` | Above the hotbar (most common) |
| `chat` | In the chat window |
| `bossbar` | Boss bar at the top of the screen |

Set this in `config.yml`:

```yaml
mob-spawning:
  mob-counter-display: actionbar
```

When all mobs are killed, a "Floor Cleared!" message replaces the counter.

---

## Spawn Behavior

Mobs spawn at calculated positions within the floor's bounding box:

- Spawn points are spread out based on the `spread-radius` to avoid stacking
- Mobs spawn `spawn-height-offset` blocks above the floor surface (default: 2.0)
- The exact count is random between `min-mobs` and `max-mobs`

---

## Spawn Delay

By default, all mobs on a floor spawn instantly. You can stagger them with `spawn-delay-ticks`:

```yaml
mob-spawning:
  spawn-delay-ticks: 10
```

With a value of `10`, mobs spawn one at a time with a 0.5-second delay between each. This creates a more dramatic entrance effect. Set to `0` for instant spawning (default).

---

## Example Setup

Here's an example of a 5-floor dungeon with increasing difficulty:

| Floor | Mob Type | Min | Max | Notes |
|-------|----------|-----|-----|-------|
| 1 | VANILLA:ZOMBIE | 2 | 4 | Easy intro floor |
| 2 | VANILLA:SKELETON | 3 | 5 | Ranged enemies |
| 3 | VANILLA:SPIDER | 4 | 6 | Fast enemies |
| 4 | VANILLA:BLAZE | 5 | 8 | Harder mob type |
| 5 | MYTHIC:BossMonster | 1 | 1 | Single boss mob |

You can set all of this through the editor tools or by editing the room's YAML file directly in `plugins/SoapsFloor/rooms/`.

---

**Previous:** [Gameplay Guide](Gameplay-Guide.md) | **Next:** [Falling Hazard](Falling-Hazard.md)
