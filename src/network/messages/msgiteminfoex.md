# MsgItemInfoEx

This message is sent by the game server to the client to display an item with additional details for a game feature (like marketplace booths). For the most part, this message resembles [MsgItemInfo](msgiteminfo.md) with the addition of price, extended action type, and optional string (seems unused in Conquer Online).

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 37 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1108 |
| 4  | UInt32 | [ID](/network/identifiers.md) | Unique identifier for the item | 10 |
| 8  | UInt32 | [Owner ID](/network/identifiers.md) | Unique identifier for the target player | 1000000 |
| 12 | UInt32 | Price | Cost of the item if vending | 100 |
| 16 | UInt32 | [Item Type](/files/content/itemtype.dat.md) | Identifies the type of item | 730001 |
| 20 | UInt16 | Amount | Current [durability](/algorithms/calculations/item-durability.md) or amount of the item | 10000 |
| 22 | UInt16 | Max Amount | Total [durability](/algorithms/calculations/item-durability.md) or amount the item can have | 10000 |
| 24 | Byte | [Action](#action-type) | How item info is extended | 1 |
| 25 | Byte | [Status](msgiteminfo.md#item-status) | Condition bit flags on the item | 0 |
| 26 | Byte | [Position](msgiteminfo.md#item-position) | Position where the item appears | 0 |
| 27 | Byte | [Socket](/algorithms/rates/item-sockets.md) 1 | The [gem](/constants/gem.md) in the first socket position | 0 |
| 28 | Byte | [Socket](/algorithms/rates/item-sockets.md) 2 | The [gem](/constants/gem.md) in the second socket position | 0 |
| 29 | Byte | Magic 1 | Reserved for rebirth magic effect | 0 |
| 30 | Byte | Magic 2 | Reserved for an unknown purpose | 0 |
| 31 | Byte | Magic 3 | Reserved for magical [plus](/algorithms/rates/item-composition.md) rating | 0 |
| 32 | UInt32 | Data | Additional attributes for the item | 0 |
| 36 | [NetStringPacker](/network/stringpacker.md) | Strings | Group of length prefixed strings | |

#### Action Type

☑️ Assumed (Soul)

| Val | Name | Description | Strings |
|:------|:--------|:--------|:--------|
| 1 | BOOTH | Vending at a player booth | |
| 2 | EQUIPMENT | Updates equipment info window | |
