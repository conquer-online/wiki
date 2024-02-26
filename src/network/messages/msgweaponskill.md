# MsgWeaponSkill

This message is sent by the game server to update the client's proficiency levels and experience.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:----|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 16 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1025 |
| 4  | UInt32 | Type | The [weapon skill type](/files/content/weaponskillname.ini.md) | 490 |
| 8  | UInt32 | Level | The new [weapon skill level](/files/content/weaponskilllevelexp.ini.md) | 1 |
| 12 | UInt32 | Exp | The new [weapon skill experience](/files/content/weaponskilllevelexp.ini.md) | 0 |
