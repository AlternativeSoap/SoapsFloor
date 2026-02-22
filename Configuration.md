# Configuration

All main settings live in `plugins/SoapsFloor/config.yml`. This page explains every option.

Use `/sf reload` to apply changes without restarting your server.

---

## General

```yaml
gui:
  enabled: true
```

| Option | Default | Description |
|--------|---------|-------------|
| `gui.enabled` | `true` | Enable or disable the GUI menu system. When disabled, all features still work through commands. |

```yaml
dont-drop-inventory: false
```

| Option | Default | Description |
|--------|---------|-------------|
| `dont-drop-inventory` | `false` | When `true`, players keep their inventory and XP on death inside rooms. |

---

## Room Defaults

These settings apply when creating new rooms. Each room can override them individually through the editor.

```yaml
default-room-settings:
  max-floors-per-room: 50
  void-y-level: -64
  starter-to-floor-gap: 5
  floor-to-floor-gap: 3
  countdown-seconds: 10
  countdown-sound: BLOCK_NOTE_BLOCK_PLING
  countdown-sound-volume: 1.0
  countdown-sound-pitch: 1.0
  countdown-final-sound: ENTITY_ENDER_DRAGON_GROWL
  countdown-final-volume: 1.0
  countdown-final-pitch: 1.2
  floor-drop-delay: 3
  auto-start-enabled: true
  waiting-timer-enabled: true
  waiting-timer-seconds: 30
  min-players: 1
  max-players: 4
  allow-join-in-progress: false
```

### Structural Settings

| Option | Default | Description |
|--------|---------|-------------|
| `max-floors-per-room` | `50` | Maximum number of floors a room can have. |
| `void-y-level` | `-64` | Y-level that counts as falling into the void. Players below this fail the dungeon. |
| `starter-to-floor-gap` | `5` | Blocks of empty space between the starter room and floor 1. |
| `floor-to-floor-gap` | `3` | Blocks of empty space between consecutive floors. |

### Countdown Settings

| Option | Default | Description |
|--------|---------|-------------|
| `countdown-seconds` | `10` | Seconds to count down before the floor drops. |
| `countdown-sound` | `BLOCK_NOTE_BLOCK_PLING` | Sound played each countdown tick. |
| `countdown-sound-volume` | `1.0` | Volume of the countdown tick sound. |
| `countdown-sound-pitch` | `1.0` | Starting pitch. Increases automatically each tick. |
| `countdown-final-sound` | `ENTITY_ENDER_DRAGON_GROWL` | Sound played when countdown hits zero. |
| `countdown-final-volume` | `1.0` | Volume of the final sound. |
| `countdown-final-pitch` | `1.2` | Pitch of the final sound. |

### Gameplay Settings

| Option | Default | Description |
|--------|---------|-------------|
| `floor-drop-delay` | `3` | Seconds to wait after mobs are cleared before dropping to the next floor. |
| `auto-start-enabled` | `true` | Automatically start the dungeon when a player enters the starter room. |
| `waiting-timer-enabled` | `true` | Enable the waiting timer before the countdown begins. |
| `waiting-timer-seconds` | `30` | How long to wait for more players before locking the room. |
| `min-players` | `1` | Minimum players needed to auto-start. Set to `1` for solo play. |
| `max-players` | `4` | Maximum players per session. Set to `0` for unlimited. |
| `allow-join-in-progress` | `false` | Whether players can join a session that already started. |

---

## Mob Spawning

```yaml
mob-spawning:
  default-min-mobs: 3
  default-max-mobs: 8
  default-mob-type: VANILLA:ZOMBIE
  default-spread-radius: 3
  spawn-delay-ticks: 0
  mob-counter-display: actionbar
```

| Option | Default | Description |
|--------|---------|-------------|
| `default-min-mobs` | `3` | Minimum mobs to spawn per floor (unless overridden per floor). |
| `default-max-mobs` | `8` | Maximum mobs to spawn per floor. |
| `default-mob-type` | `VANILLA:ZOMBIE` | Default mob type. Use `VANILLA:<type>` or `MYTHIC:<id>`. |
| `default-spread-radius` | `3` | Minimum blocks of space between mob spawn points. |
| `spawn-delay-ticks` | `0` | Ticks between each mob spawn. `0` = all spawn instantly. Set to `10` for a 0.5s delay between each mob. |
| `mob-counter-display` | `actionbar` | How remaining mobs are shown: `actionbar`, `chat`, or `bossbar`. |

---

## Anti-Cheese

Prevents players from cheating their way through floors. Admins with `soapsfloor.admin` are exempt.

```yaml
anti-cheese:
  disable-elytra: true
  block-ender-pearls: true
  block-chorus-fruit: true
  block-flying: true
  fall-damage-multiplier: 0.0
  remove-invisibility-on-join: true
  force-survival: true
  death-behavior: respawn
  blacklisted-items:
    - ENDER_EYE
```

| Option | Default | Description |
|--------|---------|-------------|
| `disable-elytra` | `true` | Prevent elytra use inside rooms. |
| `block-ender-pearls` | `true` | Block ender pearl throwing inside rooms. |
| `block-chorus-fruit` | `true` | Block Chorus Fruit random teleportation inside rooms. |
| `block-flying` | `true` | Block creative/spectator flying inside rooms. |
| `fall-damage-multiplier` | `0.0` | Fall damage multiplier. `0.0` = no fall damage, `1.0` = normal damage. |
| `remove-invisibility-on-join` | `true` | Strip invisibility potion effect when entering a room. |
| `force-survival` | `true` | Force survival mode when entering a room. Remembers the player's gamemode and restores it when the game ends. |
| `death-behavior` | `respawn` | What happens when a player dies: `kick` (removed from room), `spectate` (spectator mode), or `respawn` (respawn on current floor). |
| `blacklisted-items` | `[ENDER_EYE]` | Items that cannot be used inside dungeon rooms. Players cannot interact with, place, drop, or throw these items while in a session. Uses Bukkit Material names. |

---

## Block Protection

Built-in block protection for dungeon rooms. Admins with `soapsfloor.bypass.protection` are exempt.

```yaml
block-protection:
  enabled: true
  prevent-block-break: true
  prevent-block-place: true
  prevent-explosions: true
  prevent-bucket-use: true
```

| Option | Default | Description |
|--------|---------|-------------|
| `enabled` | `true` | Enable built-in block protection. |
| `prevent-block-break` | `true` | Prevent breaking blocks inside rooms. |
| `prevent-block-place` | `true` | Prevent placing blocks inside rooms. |
| `prevent-explosions` | `true` | Block TNT, creeper, and other explosion damage inside rooms. |
| `prevent-bucket-use` | `true` | Block bucket placement inside rooms. |

---

## PvP

```yaml
pvp-enabled: false
```

| Option | Default | Description |
|--------|---------|-------------|
| `pvp-enabled` | `false` | Allow player-vs-player damage inside dungeons. Mobs can still damage players regardless. |

---

## Falling Hazard

An optional descending particle plane that forces players to keep moving down.

```yaml
falling-hazard:
  enabled: false
  speed: 1.0
  fall-interval: 100
  damage: 2.0
  slice-height: 1.0
  render-interval: 4
  particle-density: 30
  particles-per-point: 5
  spread-horizontal: 0.8
  spread-vertical: 0.3
  particle: DUST
  color: "#FF3300"
  particle-size: 1.5
```

See the [Falling Hazard](Falling-Hazard) page for a full breakdown of these settings.

---

## Weakness System

The weakness/challenge modifier system is configured in a separate file: `plugins/SoapsFloor/weaknesses.yml`.

Weaknesses are optional difficulty modifiers that players vote on before each dungeon run. Players who complete a run under a weakness earn boosted rewards based on the weakness multiplier.

Key settings in `weaknesses.yml`:

| Option | Default | Description |
|--------|---------|-------------|
| `enabled` | `true` | Master toggle for the entire weakness system. |
| `voting.duration` | `15` | Seconds players have to vote. |
| `voting.options-count` | `3` | Number of random weakness options presented each vote. |
| `voting.allow-no-weakness` | `true` | Whether "No Weakness" is always available as a voting option. |

There are 17 built-in weaknesses across four categories:

- **Potion-based** — Blindness, Slowness, Glowing, Nausea, Mining Fatigue, Weakness, Poison, Darkness
- **Attribute-based** — Half Hearts, No Jumping, Short Reach, Heavy Gravity
- **Event-based** — No Sprint, No Shield, No Healing, Fragile Armor
- **Task-based** — Hunger Drain

Each weakness has a configurable `name`, `description`, `icon`, `multiplier`, and `enabled` toggle. See [Default Config Files](Default-Config-Files) for the full file.

---

## Effects

### Victory Effects

```yaml
victory:
  teleport-to-spawn: true
  teleport-delay: 3
  title-enabled: true
  title: "<gold><bold>DUNGEON CLEARED!</bold></gold>"
  subtitle: "<gray>Completed in <white>{time}</white></gray>"
  title-fade-in: 10
  title-stay: 70
  title-fade-out: 20
  sound: entity.player.levelup
  sound-volume: 1.0
  sound-pitch: 1.0
  victory-particle: FIREWORK
  victory-particle-count: 100
  reward-commands:
    - "say {player} completed {room} in {time}!"
```

| Option | Default | Description |
|--------|---------|-------------|
| `teleport-to-spawn` | `true` | Teleport players to spawn after winning. If the room has an exit point, it uses that instead. |
| `teleport-delay` | `3` | Seconds to wait after victory before teleporting players out. During this time players can enjoy the celebration effects. Set to `0` for instant teleport. |
| `title-enabled` | `true` | Show a title and subtitle on screen when the dungeon is cleared. |
| `title` | *see above* | Title text shown on victory. Supports MiniMessage. |
| `subtitle` | *see above* | Subtitle text shown on victory. Supports MiniMessage. Placeholder: `{time}`. |
| `title-fade-in` | `10` | Ticks for the title fade-in animation. |
| `title-stay` | `70` | Ticks the title stays on screen. |
| `title-fade-out` | `20` | Ticks for the title fade-out animation. |
| `sound` | `entity.player.levelup` | Sound played on victory. Accepts Minecraft namespaced keys or Bukkit enum names. |
| `sound-volume` | `1.0` | Volume of the victory sound. |
| `sound-pitch` | `1.0` | Pitch of the victory sound. |
| `victory-particle` | `FIREWORK` | Particle effect on victory. Options: `FIREWORK`, `TOTEM_OF_UNDYING`, `EXPLOSION`, `DRAGON_BREATH`. |
| `victory-particle-count` | `100` | Number of particles to spawn. |
| `reward-commands` | *see above* | Commands to run on victory. Placeholders: `{player}`, `{room}`, `{time}`, `{kills}`, `{floors}`. |

### Floor Drop Effects

```yaml
floor-drop:
  particle-effect: EXPLOSION
  particle-count: 50
  sound-effect: entity.generic.explode
  sound-volume: 1.0
  sound-pitch: 0.8
```

| Option | Default | Description |
|--------|---------|-------------|
| `particle-effect` | `EXPLOSION` | Particle when a floor drops. Options: `EXPLOSION`, `CLOUD`, `LARGE_SMOKE`, `CAMPFIRE_COSY_SMOKE`. |
| `particle-count` | `50` | Number of particles. |
| `sound-effect` | `entity.generic.explode` | Sound played when a floor drops. Accepts Minecraft namespaced keys or Bukkit enum names. |
| `sound-volume` | `1.0` | Volume. |
| `sound-pitch` | `0.8` | Pitch. |

---

## Editor Mode

Settings for the wand-based room editor.

```yaml
editor-mode:
  enable-previews: true
  enable-glow-outline: true
  preview-view-range: 1.0
  show-particle-borders: false
  particle-type: END_ROD
  particle-interval: 10
  wand-selection:
    show-particles: true
    max-selection-volume: 100000
    max-selection-dimension: 200
  restore-location: true
  restore-gamemode: true
  prevent-block-break: true
  prevent-block-place: true
  show-actionbar-hints: true
  actionbar-interval: 60
```

| Option | Default | Description |
|--------|---------|-------------|
| `enable-previews` | `true` | Show ghost block previews of floor positions while editing. |
| `enable-glow-outline` | `true` | Show glowing outlines on preview structures. |
| `preview-view-range` | `1.0` | Chunk render distance for previews. |
| `show-particle-borders` | `false` | Show particle borders around floor previews. |
| `particle-type` | `END_ROD` | Particle type for borders. |
| `particle-interval` | `10` | Ticks between particle updates. |
| `wand-selection.show-particles` | `true` | Show a particle outline around the selected area when setting pos1/pos2. |
| `wand-selection.max-selection-volume` | `100000` | Maximum total blocks allowed in a selection (W×H×L). |
| `wand-selection.max-selection-dimension` | `200` | Maximum blocks per axis (width, height, or length). |
| `restore-location` | `true` | Restore the player's location when leaving editor mode. |
| `restore-gamemode` | `true` | Restore the player's gamemode when leaving editor mode. |
| `prevent-block-break` | `true` | Prevent breaking blocks in editor mode. |
| `prevent-block-place` | `true` | Prevent placing blocks in editor mode. |
| `show-actionbar-hints` | `true` | Show hints in the action bar during editing. |
| `actionbar-interval` | `60` | Ticks between action bar updates (60 = 3 seconds). |

---

## Visualization

Particle markers shown to admins for debugging room elements.

```yaml
visualization:
  enabled: true
  show-bounds: true
  show-spawns: true
```

| Option | Default | Description |
|--------|---------|-------------|
| `enabled` | `true` | Enable admin visualization. |
| `show-bounds` | `true` | Show floor bounds as a wireframe. |
| `show-spawns` | `true` | Show entry/exit spawn points. |

---

## Schematic Settings

```yaml
schematic-settings:
  floor-removal-inset: 1
  spawn-height-offset: 2.0
```

| Option | Default | Description |
|--------|---------|-------------|
| `floor-removal-inset` | `1` | Blocks from the edge kept intact when a floor drops. Prevents walls from getting destroyed. |
| `spawn-height-offset` | `2.0` | Blocks above the floor surface where mobs spawn. |

---

## Debug Mode

For testing only. Do not enable on a live server.

```yaml
debug-mode:
  enabled: false
  instant-start: true
  instant-floor-drop: true
  instant-mob-spawn: true
  verbose-logging: false
```

| Option | Default | Description |
|--------|---------|-------------|
| `enabled` | `false` | Enable debug mode. |
| `instant-start` | `true` | Skip the countdown timer. |
| `instant-floor-drop` | `true` | No delay between floor drops. |
| `instant-mob-spawn` | `true` | Mobs spawn without delay. |
| `verbose-logging` | `false` | Extra output in the server console. |

---

**Previous:** [Getting Started](Getting-Started.md) | **Next:** [Room Creation Guide](Room-Creation-Guide.md)
