# Npc.ini

This file defines the 3D model, animations, and rendering properties for each NPC type. The server references NPCs by their type ID in [MsgNpcInfo](../../network/messages/msgnpcinfo.md) the client uses this file to know how to render them.

## File Format

### INI Headings

Each section header follows the format:

```
[NpcTypeX]
```

Where `X` is the NPC type ID. The client parses it by stripping the `NpcType` prefix and reading the int. 

### INI Sections

Each section defines one NPC type.

```
[NpcType1]
Name=Storekeeper
SimpleObjID=0211
StandByMotion=9990010100
BlazeMotion=9990010190
RestMotion=9990010101
Effect=none
ASB=5
ADB=6
FixDir=0
```

| Field           | Type   | Description                                                                                                       |
|:----------------|:-------|:------------------------------------------------------------------------------------------------------------------|
| `Name`          | string | Display name shown above the NPC in-game. Can be overridden by [MsgNpcInfo](../../network/messages/msgnpcinfo.md) |
| `SimpleObjID`   | uint   | ID of the object in C3 Simple Objects                                                                             |
| `StandByMotion` | int64  | Motion ID in C3 for Standing-Still NPC (Not Interacted With)                                                      |
| `BlazeMotion`   | int64  | Motion ID in C3 when Hovering-Over or Interacting with NPC                                                        |
| `RestMotion`    | int64  | Motion ID in C3 that plays periodically when on-screen & not interacting                                          |
| `Effect`        | string | Name of a 3DEffect in C3 to add to the NPC. Default is none.                                                      |
| `ASB`           | int    | Alpha Source Blend [1]                                                                                            |
| `ADB`           | int    | Alpha Destination Blend [1]                                                                                       |
| `FixDir`        | uint   | Fixed facing direction. `0` = NPC rotates to where player is on interaction. `1` = NPC stays fixed direction      |
| `ZoomPercent`   | int    | *(Optional)* Model scale as a percentage.  Defaults to `100`                                                      |


### References

[1] https://gitlab.com/conquer-online/wiki/-/wikis/Files/3DEffect.ini