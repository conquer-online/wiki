# NpcX.ini

This file defines the appearance for NPC types that are rendered as full character models with equipment, rather than the simple 3D objects.

These are NPCs which are the class promotion NPCs and dressed with weapons and armor.

## File Format

### INI Headings

Each section header follows the format:

```
[X]
```

Where `X` is the NPC type ID. Unlike [npc.ini](npc.ini.md), there is no `NpcType` prefix.

### INI Sections

Each section defines one NPC type.

```
[5000]
Name=WarriorGod
AddSize=1
Scale=120
FixDir=0
Look=500
Head=0
Hair=0
Armet=111300
Armor=0
RWeapon=560439
LWeapon=900309
Misc=0
Mount=0
Effect=foot03
```

| Field        | Type   | Description                                                                                                                                                                       |
|:-------------|:-------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Name`       | string | Display name shown above the NPC in-game. Can be overridden by [MsgNpcInfo](../../network/messages/msgnpcinfo.md)                                                                 |
| `AddSize`    | int    | Unknown, always 1.                                                                                                                                                                |
| `Scale`      | uint   | Model scale as a percentage. Defaults to `100`                                                                                                                                    |
| `FixDir`     | uint   | Fixed facing direction. `0` = NPC rotates to where player is on interaction. `1` = NPC stays fixed direction                                                                      |
| `Look`       | uint   | This is the overall look of the NPC (body & armor) from C3 under `mix_body`                                                                                                       |
| `Head`       | uint   | Seems to always be zero, as Armet takes precedence (and no Head items in C3)                                                                                                      |
| `Hair`       | uint   | Seems to always be zero, as Armet takes precedence. But can be [Hairstyle](../../constants/hairstyles.md)                                                                         |
| `Armet`      | uint   | Helmet item ID. `0` = none.                                                                                                                                                       |
| `ArmetColor` | int    | Color/quality value prepended (as `00X`) to the Armet ID to form the C3 mesh path. e.g. ArmetColor=`3` + Armet=`111300` == `c3/mesh/003111300`. Defaults to `3` if not specified. |
| `Armor`      | uint   | Seems to always be zero, as look takes precedence.                                                                                                                                |
| `ArmorColor` | int    | The armor quality, by default this is 3. Unused as Armor is zero.                                                                                                                 |
| `RWeapon`    | uint   | Right-hand weapon item ID. `0` = none.                                                                                                                                            |
| `LWeapon`    | uint   | Left-hand weapon item ID. `0` = none.                                                                                                                                             |
| `Misc`       | uint   | Always 0, there's only one Misc in C3 and unrelated to this.                                                                                                                      |
| `Mount`      | uint   | Always 0, but can be set to a mount from C3 (`8010001`) - but breaks the model                                                                                                    |
| `Effect`     | string | Name of a 3DEffect in C3 to add to the NPC. Default is none.                                                                                                                      |
