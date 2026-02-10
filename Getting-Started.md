# Getting Started

This page walks you through installing SoapsFloor and creating your first dungeon room.

---

## Installation

1. Download the latest `SoapsFloor.jar`
2. Place it in your server's `plugins/` folder
3. Make sure **WorldEdit** or **FastAsyncWorldEdit (FAWE)** is installed. FAWE is recommended.
4. Start (or restart) your server
5. The plugin will generate its config files automatically

You should see this in your console:

```
[SoapsFloor] SoapsFloor has been enabled!
```

---

## Prepare Your Schematics

Before you can create a dungeon room, you need at least one floor schematic.

We recommend using [FastAsyncWorldEdit (FAWE)](https://www.spigotmc.org/resources/fastasyncworldedit.13932/) instead of regular WorldEdit. FAWE is what the plugin is built and tested with, and it handles large schematics much better.

1. Build a floor layout in your world (a flat platform with walls, obstacles, etc.)
2. Select it with WorldEdit (`//wand`, left-click one corner, right-click the other)
3. Copy the selection: `//copy`
4. Save it: `//schem save my_floor`
5. Copy the `.schem` file from `plugins/FastAsyncWorldEdit/schematics/` (or `plugins/WorldEdit/schematics/` if using regular WorldEdit) into `plugins/SoapsFloor/schematics/`

> You must `//copy` before `//schem save`, otherwise the schematic will be empty.

> Each schematic represents one floor layout. Players will be dropped onto this platform and fight mobs there.

---

## Create Your First Room

### Step 1: Get the Wand

Run this command:

```
/sf wand create my_dungeon
```

This gives you the **Room Setup Wand** and puts you in editor mode. Your inventory is saved and will be restored when you leave the editor.

### Step 2: Select the Starter Area

The starter area is where players spawn before the dungeon begins. It sits above all the floors.

- **Right-click** a block to set **Position 1**
- **Left-click** a block to set **Position 2**

This defines the bounding box of your starter room.

### Step 3: Set Entry and Exit Points

After selecting the starter area:

- **Right-click** a block to set the **entry point** (where players spawn when they join)
- **Right-click** another block to set the **exit point** (where players teleport after winning)

### Step 4: Add Floors

Type the schematic name in chat to add a floor:

```
my_floor
```

This adds Floor 1 using the `my_floor` schematic. Keep typing schematic names to add more floors.

To assign one schematic to multiple floors at once:

```
my_floor 1-5
```

This assigns `my_floor` to floors 1 through 5.

### Step 5: Configure Settings (Optional)

While in editor mode, your hotbar has adjustment tools:

| Slot | Tool | What It Does |
|------|------|-------------|
| 1 | Room Setup Wand | Select positions |
| 2 | Floor Selector | Switch between floors to configure them |
| 3 | Mob Settings | Set mob type and count per floor |
| 4 | Starter Gap Adjuster | Gap between starter room and floor 1 |
| 5 | Floor Gap Adjuster | Gap between consecutive floors |
| 6 | Max Players Adjuster | Set max players per session |
| 7 | Countdown Adjuster | Set countdown timer duration |
| 8 | Settings Info | Reference guide |
| 9 | Custom Commands | Set commands to run per floor |
| 10 | How-To Guide Book | Written book guide in main inventory |

**Right-click** to increase a value, **left-click** to decrease it. Hold **shift** for larger increments.

### Step 6: Save the Room

When you're done, type in chat:

```
done
```

Or use the command:

```
/sf wand finish
```

Your room is saved and ready to play.

---

## Test Your Room

Join the room you just created:

```
/sf room my_dungeon
```

You'll be teleported to the starter area. After the waiting timer and countdown, the floor drops and the dungeon begins.

To leave at any time:

```
/sf room leave
```

---

## What's Next

- [Room Creation Guide](Room-Creation-Guide) - Detailed walkthrough of every editor tool
- [Configuration](Configuration) - Customize timers, mob counts, effects, and more
- [Mob System](Mob-System) - Set up different mobs per floor
- [Commands & Permissions](Commands-and-Permissions) - Full command reference

---

**Previous:** [Introduction](Introduction) | **Next:** [Configuration](Configuration)

