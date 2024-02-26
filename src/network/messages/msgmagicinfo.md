# MsgMagicInfo

This game server message is sent to the client to describe spells the player has learned. [MagicType.dat](/files/content/MagicType.dat.md) contains all spells accompanied with available levels and experience required for the next level, used to fill this message.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 12 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1103 |
| 4  | UInt32 | Exp | Current experience towards leveling the spell | 0 |
| 8  | UInt16 | Type | Magic type identifier | 1001 |
| 10 | UInt16 | Level | Level of the spell | 1 |
