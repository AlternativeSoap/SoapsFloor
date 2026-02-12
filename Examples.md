# Examples

Practical setups for common scenarios.

---

## Example 1: Simple 3-Floor Dungeon

A quick dungeon for beginners. Three floors of zombies.

### Setup

1. Build a simple 15x15 stone platform with walls
2. Save it as a schematic: `//schem save basic_floor`
3. Copy the `.schem` file to `plugins/SoapsFloor/schematics/`

### Create the Room

```
/sf wand create beginner_dungeon
```

1. Select a starter area above where you want the dungeon
2. Set entry and exit points
3. In chat, type: `basic_floor 1-3`
4. Type `done`

### Result

- 3 floors, all using the same layout
- Default mobs (3-8 zombies per floor)
- Solo or up to 4 players

---

## Example 2: 10-Floor Mixed Dungeon

A more advanced setup with different schematics and mob types per floor.

### Schematics Needed

- `open_arena` - A wide open arena
- `corridor_maze` - Narrow corridors
- `boss_room` - A large boss chamber

### Create the Room

```
/sf wand create gauntlet
```

1. Select the starter area and spawn points
2. Add floors:
   ```
   open_arena 1-3
   corridor_maze 4-7
   open_arena 8-9
   boss_room 10
   ```
3. Use the **Floor Selector** and **Mob Settings** to customize each floor:

| Floor | Mob Type | Min | Max |
|-------|----------|-----|-----|
| 1-3 | VANILLA:ZOMBIE | 3 | 5 |
| 4-7 | VANILLA:SKELETON | 4 | 7 |
| 8-9 | VANILLA:BLAZE | 5 | 8 |
| 10 | MYTHIC:DungeonBoss | 1 | 1 |

4. Type `done`

---

## Example 3: Multiplayer Competitive Room

A room designed for parties of 2-4 players competing for the fastest clear time.

### Config Changes

In `config.yml`:

```yaml
default-room-settings:
  min-players: 2
  max-players: 4
  waiting-timer-seconds: 60
  countdown-seconds: 5
```

### Reward Commands

```yaml
victory:
  reward-commands:
    - "say {player} completed {room} in {time}!"
    - "eco give {player} 500"
    - "crate givekey {player} dungeon_key 1"
```

This gives players 500 coins and a crate key on victory.

---

## Example 4: Falling Hazard Dungeon

A dungeon where players are pressured by a descending damage plane.

### Config Changes

```yaml
falling-hazard:
  enabled: true
  speed: 1.0
  fall-interval: 80
  damage: 3.0
  slice-height: 1.5
  particle: FLAME
```

This creates an aggressive flame wall that drops every 4 seconds and deals 1.5 hearts of damage.

Pair this with faster mobs (skeletons, spiders) to ramp up the difficulty.

---

## Example 5: Custom Commands Per Floor

Run commands when specific floors start. Useful for effects, messages, or spawning extra entities.

### During Room Creation

Select each floor and add commands:

**Floor 1:**
```
title {player} subtitle {"text":"The dead are rising...","color":"gray"}
```

**Floor 5 (midway point):**
```
title {player} subtitle {"text":"Halfway there!","color":"gold"}
give {player} golden_apple 1
```

**Floor 10 (boss floor):**
```
title {player} subtitle {"text":"Face the boss!","color":"red","bold":true}
playsound entity.wither.spawn master {player} ~ ~ ~ 1 0.8
```

---

## Example 6: Event Dungeon with Reset

For server events, you might want a timed dungeon that resets automatically.

### Setup

1. Create the room normally
2. Set `max-players: 1` for solo competition
3. Configure reward commands for the event:

```yaml
victory:
  reward-commands:
    - "say {player} cleared the event dungeon in {time}!"
    - "lp user {player} permission settemp event.winner true 7d"
```

Players can run `/sf room event_dungeon` as many times as they want, competing for the best time on the leaderboard.

---

## Example 7: Per-Room Settings Override

Each room's settings can be different from the global defaults. When editing a room:

- Use the **Countdown Adjuster** (slot 7) to make one room have a shorter countdown
- Use the **Max Players Adjuster** (slot 6) to allow more players in a specific room
- Use the **Gap Adjusters** (slots 4-5) to change floor spacing for a specific room

These per-room settings are saved in the room's YAML file and always override the global config.

---

**Previous:** [Commands & Permissions](Commands-and-Permissions) | **Next:** [Default Config Files](Default-Config-Files)

