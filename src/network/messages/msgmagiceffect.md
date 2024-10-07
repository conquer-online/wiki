# MsgMagicEffect

This game server message is sent to the client to display a damaging magical effect from a target or cell coordinate on one or many targets. [MagicType.dat](../../files/content/MagicType.dat.md) contains all spell types that can be sent with this message.

In later versions of the client, the target coordinates are lightly encrypted. See [MsgInteract](msginteract.md) for details.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 36 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1105 |
| 4  | UInt32 | User | [Unique identifier](../identifiers.md) of the role | 1000000 |
| 8  | UInt32 | Target | [Unique identifier](../identifiers.md) of the target or a coordinate  | `LOW:` 320 `HIGH:` 460 |
| 12 | UInt16 | [Type](../../files/content/MagicType.dat.md) | Type of magic being cast | 1001 |
| 14 | UInt16 | Level | Level of the magic being cast | 1 |
| 16 | UInt32 | Effect Num | Number of effects to display | 1 |
| 20 | [RoleInfo](#magic-effect-role-info)[] | Effects | Effects to display on roles | |

#### Magic Effect Role Info

🚩 Incomplete

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt32 | Role | [Role ID](../identifiers.md) of the target in the area effect | 1000001 |
| 1  | UInt32 | Data | Damage associated with the area effect | 1 |
| 2  | UInt32 | Reserved | Unknown | 0 |
