# Falling Hazard

The falling hazard is an optional feature that adds a descending plane of particles above players. It forces them to keep fighting and moving instead of camping at the top of a floor.

---

## How It Works

When enabled, a horizontal sheet of particles spawns at the ceiling of each floor and slowly descends:

- **Players above the plane** are instantly killed
- **Players inside the plane** (within the slice height) take damage every tick
- **Players below the plane** are safe

The hazard resets to the ceiling whenever the session moves to a new floor.

---

## Enabling the Hazard

In `config.yml`:

```yaml
falling-hazard:
  enabled: true
```

That's it. The hazard will activate on every floor for every room. Set it to `false` to disable.

---

## Configuration

All settings are in the `falling-hazard` section of `config.yml`:

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

### Movement

| Option | Default | Description |
|--------|---------|-------------|
| `speed` | `1.0` | How many blocks the hazard drops per fall interval. |
| `fall-interval` | `100` | Ticks between each drop step. 100 ticks = 5 seconds per drop. Lower = faster descent. |

### Damage

| Option | Default | Description |
|--------|---------|-------------|
| `damage` | `2.0` | Damage dealt per render tick to players inside the slice (in half-hearts). |
| `slice-height` | `1.0` | Thickness of the damage zone in blocks. |

### Particle Rendering

| Option | Default | Description |
|--------|---------|-------------|
| `render-interval` | `4` | Ticks between particle refreshes. Lower = smoother but more lag. |
| `particle-density` | `30` | Grid resolution. Total particles per refresh is roughly density squared. |
| `particles-per-point` | `5` | How many particles spawn at each grid point. |
| `spread-horizontal` | `0.8` | Horizontal spread per point in blocks. |
| `spread-vertical` | `0.3` | Vertical spread per point in blocks. |

### Particle Appearance

| Option | Default | Description |
|--------|---------|-------------|
| `particle` | `DUST` | Particle type. See below for options. |
| `color` | `#FF3300` | Hex color for color-based particles. |
| `particle-size` | `1.5` | Size multiplier for DUST particles. |

### Particle Types

**Simple particles** (no extra config needed):
- `FLAME`
- `SOUL_FIRE_FLAME`
- `END_ROD`
- `SMOKE`
- `CLOUD`

**Color particles** (use `color` and `particle-size`):
- `DUST` - Colored dust, supports hex color and size
- `DUST_COLOR_TRANSITION` - Transitioning colored dust
- `ENTITY_EFFECT` - Entity effect particles

---

## Tuning Tips

**For a slow, atmospheric hazard:**
```yaml
speed: 0.5
fall-interval: 200
damage: 1.0
particle: SOUL_FIRE_FLAME
```

**For an aggressive, fast hazard:**
```yaml
speed: 2.0
fall-interval: 40
damage: 4.0
particle: FLAME
```

**For a visual-only warning layer (no damage):**
```yaml
speed: 1.0
damage: 0.0
particle: CLOUD
```

---

## Performance

The hazard uses particles which can impact performance on larger floors. If you notice lag:

- Increase `render-interval` (less frequent updates)
- Decrease `particle-density` (fewer particles per refresh)
- Decrease `particles-per-point` (fewer particles per grid point)

---

**Previous:** [Mob System](Mob-System) | **Next:** [GUI Menus](GUI-Menus)
