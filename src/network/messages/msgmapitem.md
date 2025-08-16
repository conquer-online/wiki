# MsgMapItem

This game server message is sent to the client to display an action with an item on the map floor. It also allows the server to set "traps", which act as magic effects on a map tile and are used for squama rewards.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5095](#patch-5095)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 18 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1101 |
| 4  | UInt32 | [ID](../identifiers.md) | Map item identifier | 1 |
| 8  | UInt32 | Type | Map item type or trap [look](../../files/content/mapmagicitem.ini.md) | 0 |
| 12 | UInt16 | Pos X | X coordinate of the item or trap | 320 |
| 14 | UInt16 | Pos Y | Y coordinate of the item or trap | 460 |
| 16 | UInt16 | [Action](#action-type) | How to process the message | 1 |

#### Action Type

☑️ Assumed (Observed) - CoFuture + Soul

| Val | Name | Description | Recipient | ID | Type |
|:----|:--------|:--------|:--------|:--------|:--------|
| 1  | CREATE | Create map item | Client | [Map Item ID](../identifiers.md) | [Item Type](../../files/content/itemtype.dat.md) |
| 2  | DELETE | Delete map item | Client | [Map Item ID](../identifiers.md) | |
| 3  | PICK | Request to pick up map item | Server | [Map Item ID](../identifiers.md) | |
| 10 | CAST_TRAP | Place a floor trap | Client | [Trap ID](../identifiers.md) | [Look](../../files/content/mapmagicitem.ini.md) |
| 11 | SYNCHRO_TRAP | Update a floor trap | Client | [Trap ID](../identifiers.md) | [Look](../../files/content/mapmagicitem.ini.md) |
| 12 | DROP_TRAP | Stop a floor trap | Client | [Trap ID](../identifiers.md) | |

## Patch 5095

#### Message Definition

☑️ Assumed (Observed) - Elite-CoEmu

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 24 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1101 |
| 4  | UInt32 | [ID](../identifiers.md) | Map item identifier | 1 |
| 8  | UInt32 | Type | Map item type or trap [look](../../files/content/mapmagicitem.ini.md) | 0 |
| 12 | UInt16 | Pos X | X coordinate of the item or trap | 320 |
| 14 | UInt16 | Pos Y | Y coordinate of the item or trap | 460 |
| 16 | UInt16 | [Color](msgiteminfo.md#item-color) | Color modifier for the item | 3 |
| 18 | UInt16 | [Action](#action-type) | How to process the message | 1 |
| 20 | UInt32 | Unused | Confirmed unused by the client | 0 |

#### Action Type

☑️ Assumed (Observed) - Elite-CoEmu

| Val | Name | Description | Recipient | ID | Type |
|:----|:--------|:--------|:--------|:--------|:--------|
| 1  | CREATE | Create map item | Client | [Map Item ID](../identifiers.md) | [Item Type](../../files/content/itemtype.dat.md) |
| 2  | DELETE | Delete map item | Client | [Map Item ID](../identifiers.md) | |
| 3  | PICK | Request to pick up map item | Server | [Map Item ID](../identifiers.md) | |
| 4  | PICK_EFFECT | Pick up item with an effect | Client | [Map Item ID](../identifiers.md) | |
| 10 | CAST_TRAP | Place a floor trap | Client | [Trap ID](../identifiers.md) | [Look](../../files/content/mapmagicitem.ini.md) |
| 11 | SYNCHRO_TRAP | Update a floor trap | Client | [Trap ID](../identifiers.md) | [Look](../../files/content/mapmagicitem.ini.md) |
| 12 | DROP_TRAP | Stop a floor trap | Client | [Trap ID](../identifiers.md) | |
