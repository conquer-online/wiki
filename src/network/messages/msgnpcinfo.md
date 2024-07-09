# MsgNpcInfo

This message is sent by the game server to the client to spawn an NPC into the world.

The lookface of an NPC is as calculated:

```csharp
Lookface = Type * 10 + Direction
```

The type portion of the lookface can be found in [npc.ini](/files/content/npc.ini.md). This file is also what determines the name of the NPC.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 18 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 2030 |
| 4  | UInt32 | [ID](/network/identifiers.md) | Unique identifier | 1 |
| 8  | UInt16 | X | X coordinate of the NPC | 320 |
| 10 | UInt16 | Y | Y coordinate of the NPC | 460 |
| 12 | UInt16 | [Role](/constants/roletype.md) | The role the NPC plays | 1 |
| 14 | UInt16 | Lookface | The type and direction of the NPC | 10 |
| 16 | UInt16 | [Sort](#npc-sort-flags) | Sort flags or [action type](/constants/actions.md) the NPC performs | 1 |
| 18 | [NetStringPacker](/network/stringpacker.md) | Strings | Optional name of the NPC | |

#### NPC Sort Flags

☑️ Assumed (Observed) - CoFuture + Soul

| Val | Name | Description | Strings |
|:------|:--------|:--------|:--------|
| 0 | NONE | NPC that responds as dialog | |
| 1 | TASK | NPC that opens a window in the client  | |
| 2 | RECYCLE | NPC that is dynamically relocated | |
