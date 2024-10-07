# MsgFlushExp

This game server message is sent to the client to update the interface with new weapon skill, magic, XP skill, or other types of experience.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 12 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1104 |
| 4  | UInt32 | Exp | Updated experience towards leveling the spell | 0 |
| 8  | UInt16 | Type | Magic or skill type identifier | 1001 |
| 10 | UInt16 | [Action](#action-type) | The type of experience being updated | 0 |

#### Action Type

☑️ Assumed (Soul)

| Val | Name | Description | File |
|:----|:--------|:--------|:--------|
| 0 | WEAPON_SKILL | Weapon skill proficiency | [WeaponSkillLevelExp.ini](../../files/content/weaponskilllevelexp.ini.md) |
| 1 | MAGIC | Magic spell experience | [MagicType.dat](../../files/content/MagicType.dat.md) |
