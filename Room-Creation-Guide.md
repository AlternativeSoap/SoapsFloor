# Room Creation Guide

This page covers the full room creation process in detail, including every editor tool and all the options available to you.

---

## Overview

Creating a room involves these steps:

1. Start a wand session
2. Select the starter area
3. Set entry and exit spawn points
4. Add floor schematics
5. Configure per-floor settings (mobs, commands, gaps)
6. Save the room

The entire process happens in **editor mode**, which gives you a clean workspace with specialized tools in your hotbar.

---

## Starting Editor Mode

### Creating a New Room

```
/sf wand create <room_id>
```

This starts a new room from scratch. The room ID is the name used in commands and config files. Keep it simple and lowercase (e.g., `arena`, `dungeon_1`, `boss_tower`).

### Editing an Existing Room

```
/sf wand edit <room_id>
```

Opens an existing room for editing. All current settings and floors are loaded into the session.

### What Happens When You Enter Editor Mode

- Your current inventory is saved and cleared
- Your location and gamemode are saved
- You're set to Creative mode with flight enabled
- Your hotbar is filled with editor tools
- Action bar hints guide you through each step

---

## Step 1: Select the Starter Area

The starter area is the room where players spawn and wait before the dungeon begins. It sits at the top of the dungeon.

With the **Room Setup Wand** (slot 1):

- **Right-click** a block to set **Position 1** (one corner)
- **Left-click** a block to set **Position 2** (opposite corner)

This defines the bounding box of the starter room. The floor of this area will be removed when the dungeon starts, dropping players to Floor 1.

> Make sure the starter area is large enough for your max player count. The floor should be solid since it gets destroyed to drop players.

---

## Step 2: Set Spawn Points

After selecting the starter area:

- **Right-click** a block to set the **entry point** (where players teleport when joining)
- **Right-click** another block to set the **exit point** (where players teleport after winning)

The entry point should be inside the starter area. The exit point can be anywhere you want players to end up after completing the dungeon.

---

## Step 3: Add Floors

Once the starter area and spawn points are set, you'll be prompted to add floors.

### Adding a Single Floor

Type the schematic name in chat:

```
my_floor
```

This creates the next floor using that schematic.

### Adding Multiple Floors at Once

Assign one schematic to a range of floors:

```
my_floor 1-5
```

This assigns `my_floor` to floors 1 through 5.

### Assigning a Schematic to a Specific Floor

```
boss_arena 10
```

This sets floor 10 to use the `boss_arena` schematic.

### Viewing Current Floors

Type `list` in chat or use:

```
/sf wand floors
```

This shows all configured floors with their schematics and mob spawn counts.

### Overwriting a Floor

If a floor already has a schematic, you'll be asked to confirm:

```
confirm <schematic> <floor>
```

---

## Step 4: Editor Hotbar Tools

While in editor mode, your hotbar contains these tools:

### Slot 1: Room Setup Wand
Used to select the starter area positions. Right-click for position 1, left-click for position 2.

### Slot 3: How-To Guide Book
A written book with step-by-step instructions. Open it any time you need a reference.

### Slot 4: Starter Gap Adjuster
Controls the vertical gap between the starter room and Floor 1.
- **Right-click:** Increase gap
- **Left-click:** Decrease gap
- Hold **Shift** for larger increments

### Slot 5: Floor Gap Adjuster
Controls the vertical gap between consecutive floors.
- **Right-click:** Increase gap
- **Left-click:** Decrease gap
- Hold **Shift** for larger increments

### Slot 6: Max Players Adjuster
Sets the maximum number of players allowed in this room.
- **Right-click:** Increase
- **Left-click:** Decrease

### Slot 7: Countdown Adjuster
Sets the countdown duration (in seconds) before the floor drops.
- **Right-click:** Increase
- **Left-click:** Decrease

### Slot 8: Floor Selector
Lets you switch between floors to configure them individually.
- **Right-click:** Next floor
- **Left-click:** Previous floor

The selected floor is what gets modified by the Mob Settings tool.

### Slot 9: Mob Settings
Configures mob spawning for the currently selected floor.
- **Right-click:** Open mob type selection (type in chat: `vanilla:zombie` or `mythicmobs:FireDemon`)
- **Left-click:** Cycle through min/max mob count adjustments
- Hold **Shift** for larger increments

---

## Step 5: Custom Commands Per Floor

While in editor mode, you can assign custom commands that run when a specific floor starts.

Select a floor using the **Floor Selector** (slot 8), then use the **Custom Commands** tool:

- **Right-click:** Add commands (type them one by one in chat, then type `done`)
- **Left-click:** View current commands
- **Shift + Left-click:** Clear all commands for that floor

### Available Placeholders

| Placeholder | Replaced With |
|-------------|---------------|
| `{player}` | Player's name |
| `{floor}` | Current floor number |
| `{room}` | Room ID |

### Example Commands

```
give {player} diamond_sword 1
title {player} title {"text":"Floor {floor}!","color":"red"}
playsound entity.wither.spawn master {player}
```

Commands run as console, so they have full permissions.

---

## Step 6: Save the Room

When everything is configured, type `done` in chat or run:

```
/sf wand finish
```

Your room is saved to `plugins/SoapsFloor/rooms/<room_id>.yml` and is immediately playable.

### Cancelling

To exit without saving:

```
/sf wand cancel
```

Your inventory and position are restored either way.

---

## Checking Session Status

At any point during editing, use:

```
/sf wand status
```

This shows your current step, room ID, floor count, and whether the starter room is configured.

---

## Deleting a Room

```
/sf wand remove <room_id>
```

or

```
/sf room delete <room_id>
```

This permanently deletes the room's config file. You cannot delete a room while players are inside it.

---

## Tips

- Build your schematics with clear, flat floors so the removal zone works well
- The `floor-removal-inset` setting in config.yml controls how much of the floor edge stays intact when dropping. Set it to `1` to keep walls standing.
- Use the preview system (`enable-previews: true` in config) to see where floors will be placed before saving
- Test your rooms after creating them to make sure gaps and spawn points feel right
- You can always re-edit a room with `/sf wand edit <room_id>` to adjust settings later

---

**Previous:** [Configuration](Configuration) | **Next:** [Gameplay Guide](Gameplay-Guide)
