# MsgSyncAction

Synchronizes the movement of multiple players. At time of writing this, only two players can be synchronized.

Synchronized actions were introduced as part of the couple interaction system. These actions are controlled using [MsgInteract](msginteract.md) to request, accept, reject, perform, and end a synchronized action. This message is how synchronized movements are displayed to observing clients and the target of the interaction.

## Table of Contents

* [Patch 5127](#patch-5127)

## Patch 5127

#### Message Definition

☑️ Assumed (Observed)

For walking:

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 24 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1114 |
| 4  | UInt16 | [Action](#action-type) | The synchronized action | 0 |
| 6  | Byte | [Direction](../../algorithms/calculations/direction.md) | Action direction | 0 |
| 7  | Byte | [Movement Mode](#movement-modes-1) | Type of ground movement | 1 |
| 12 | UInt32 | Amount | Amount of players | 2 |
| 16 | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 20 | UInt32 | [Target](../identifiers.md) | Unique identifier for the target | 1000001 |

For jumping:

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 24 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1114 |
| 4  | UInt16 | [Action](#action-type) | The synchronized action | 0 |
| 6  | UInt16 | X | X coordinate of the action | 320 |
| 8  | UInt16 | Y | Y coordinate of the action | 460 |
| 10 | UInt16 | [Direction](../../algorithms/calculations/direction.md) | Action direction | 0 |
| 12 | UInt32 | Amount | Amount of players | 2 |
| 16 | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 20 | UInt32 | [Target](../identifiers.md) | Unique identifier for the target | 1000001 |

#### Action Type

✅ Verified (Client)

| Val | Name | Description |
|:------|:--------|:--------|
| 0 | SYNC_DIRECTION | Change direction as a couple |
| 1 | SYNC_WALK | Step as a couple |
| 2 | SYNC_JUMP | Jump as a couple |