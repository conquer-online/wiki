# MsgNpcInfoEx

This message is sent by the game server to the client to spawn an NPC with health, an extension of [MsgNpcInfo](msgnpcinfo.md). This is normally used for spawning terrain NPCs, such as the guild gate or pole during guild wars.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 36 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1109 |
| 4  | UInt32 | [ID](/network/identifiers.md) | Unique identifier | 6701 |
| 8  | UInt32 | Max Life | Maximum health of the NPC | 10000000 |
| 12 | UInt32 | Life | Current health of the NPC | 10000000 |
| 16 | UInt16 | X | X coordinate of the NPC | 163 |
| 18 | UInt16 | Y | Y coordinate of the NPC | 211 |
| 20 | UInt16 | [Role](/constants/roletype.md) | The role the NPC plays | 26 |
| 22 | UInt16 | [Lookface](msgnpcinfo.md) | The type and direction of the NPC | 241 |
| 24 | UInt16 | [Sort](msgnpcinfo.md#npc-sort-flags) | Sort flags or [action type](/constants/actions.md) the NPC performs | 1 |
| 26 | [NetStringPacker](/network/stringpacker.md) | Strings | Optional name of the NPC | 1 8 LeftGate |
