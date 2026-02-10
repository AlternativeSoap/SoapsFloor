# Gameplay Guide

This page explains the full gameplay flow from a player's perspective, from joining a room to victory (or defeat).

---

## Joining a Room

Players can join a room in three ways:

### By Command
```
/sf room <room_id>
```

### Through the GUI
Open the main menu with `/sf menu`, then click **Room Browser** to pick a room.

### Quick Join
Click **Quick Join** in the main menu to instantly join a random available room.

---

## The Gameplay Flow

Here's what happens from the moment you join until the run ends:

### 1. Entering the Starter Room

When a player joins, they're teleported to the room's **entry point** inside the starter area. A welcome message shows:

- Room name
- Total floors
- Estimated total mobs
- Difficulty rating

**Difficulty is based on floor count:**

| Floors | Difficulty |
|--------|-----------|
| 1-3 | Easy |
| 4-6 | Medium |
| 7-9 | Hard |
| 10-14 | Extreme |
| 15+ | Nightmare |

### 2. Waiting for Players

If `waiting-timer-enabled` is on, the room waits for more players to join before starting.

- The waiting time is shown in chat
- New players joining are announced to everyone in the room
- Once the timer expires, the room **locks** and no more players can join
- If `min-players` is set to `1`, a solo player can start immediately

### 3. Countdown

After the waiting timer ends (or immediately if disabled), a countdown begins:

- A title appears on screen showing the remaining seconds
- A sound plays each tick, increasing in pitch
- When it hits zero, a final sound plays and the text "GO!" appears

### 4. Floor Drop

The floor of the starter room is destroyed. Players fall down to **Floor 1**.

- Particle and sound effects play when the floor breaks
- Players get 3 seconds of invulnerability after dropping

### 5. Fighting Mobs

Mobs spawn on the floor. The remaining mob count is displayed via the configured display method (action bar, chat, or boss bar).

- Players must kill all mobs to clear the floor
- Block breaking and placing is disabled during runs
- Anti-cheese protections prevent flying, elytra, and ender pearls

### 6. Floor Cleared

Once all mobs on the floor are dead:

- A "Floor Cleared!" message appears
- A countdown begins for the next floor drop
- Custom commands for the next floor trigger (if configured)
- The current floor breaks and players fall to the next one

### 7. Repeat

Steps 5-6 repeat for each floor until all floors are cleared or all players die.

### 8. Victory

When the final floor is cleared:

- A victory screen appears with stats:
  - Completion time
  - Total mobs defeated
  - Player contributions (in multiplayer, each player's kill count and percentage)
  - Floors cleared
- Victory particle effects play
- Reward commands execute
- Players are teleported to the exit point (or world spawn)

### 9. Defeat

If a player dies or falls into the void:

- **`death-behavior: kick`** - Player is removed from the room
- **`death-behavior: spectate`** - Player enters spectator mode and can watch others finish
- **`death-behavior: respawn`** - Player respawns on the current floor

If all players die or leave, the session ends. All pasted schematics are cleaned up and the room is restored.

---

## Multiplayer

SoapsFloor supports multiplayer sessions:

- Multiple players can join the same room
- The waiting timer lets players gather before starting
- Kill contributions are tracked per player
- The victory screen shows everyone's stats ranked by kills
- All players must clear mobs together on each floor

### Player Limits

- `min-players`: Minimum needed to start (default: 1)
- `max-players`: Maximum per session (default: 4, set `0` for unlimited)
- `allow-join-in-progress`: Whether players can join after the run started (default: false)

---

## Leaving a Room

At any time during a run:

```
/sf room leave
```

Or click **Leave Session** in the main menu.

Your progress for that run is lost.

---

## Anti-Cheese Protections

These prevent players from bypassing the dungeon challenge:

| Protection | Default | What It Does |
|-----------|---------|--------------|
| Disable Elytra | On | Prevents gliding between floors |
| Block Ender Pearls | On | Prevents teleporting with pearls |
| Block Flying | On | Prevents creative/spectator flight |
| No Fall Damage | On | `0.0` multiplier by default so floor drops don't kill players |
| Block Breaking | On | Can't break blocks during a run |
| Block Placing | On | Can't place blocks during a run |

Admins with `soapsfloor.admin` bypass all restrictions.

---

## Stats Tracking

Every run tracks:

- **Total kills** across all rooms
- **Games completed**
- **Best time per room** (only counts completed runs)
- **Best kills per room** (highest kill count in a single run)

View your stats with `/sf stats` or the Stats page in the GUI menu.

---

**Previous:** [Room Creation Guide](Room-Creation-Guide) | **Next:** [Mob System](Mob-System)
