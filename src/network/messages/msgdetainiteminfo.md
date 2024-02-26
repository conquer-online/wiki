# MsgDetainItemInfo

This message is sent to the client to show an item in the detained items window. Along with a summary of the item's details (similar to [MsgItemInfo](msgiteminfo.md)), it also contains the cost of reclaiming the item, days remaining until the hunter is rewarded, and the name and identifier of the original owner and hunter.

## Table of Contents

* [Patch 5103](#patch-5103)

## Patch 5103

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 112 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1034 |
| 4  | UInt32 | Reward ID | Unique identifier of the reward record | 103 |
| 8  | UInt32 | [Item ID](/network/identifiers.md) | Unique identifier for the item (unless someone else's item) | 1 |
| 12  | UInt32 | [Item Type](/files/content/itemtype.dat.md) | Identifies the type of item | 730001 |
| 16 | UInt16 | Amount | Current [durability](/algorithms/calculations/item-durability.md) or amount of the item | 10000 |
| 18 | UInt16 | Max Amount | Total [durability](/algorithms/calculations/item-durability.md) or amount the item can have | 10000 |
| 20 | Byte | [Action](#action-type) | How item info should be processed | 1 |
| 21 | Byte | [Status](msgiteminfo.md#item-status) | Condition bit flags on the item | 0 |
| 22 | Byte | [Position](msgiteminfo.md#item-position) | Position where the item appears | 0 |
| 24 | UInt32 | [Socket](/algorithms/rates/item-sockets.md) Progress | Progress on creating a socket | 0 |
| 28 | Byte | [Socket](/algorithms/rates/item-sockets.md) 1 | The [gem](/constants/gem.md) in the first socket position | 0 |
| 29 | Byte | [Socket](/algorithms/rates/item-sockets.md) 2 | The [gem](/constants/gem.md) in the second socket position | 0 |
| 30 | Byte | Magic 1 | Reserved for rebirth magic effect | 0 |
| 31 | Byte | Magic 2 | Reserved for an unknown purpose | 0 |
| 32 | Byte | Magic 3 | Reserved for magical [plus](/algorithms/rates/item-composition.md) rating | 0 |
| 33 | Byte | Bless | Reduced damage percentage taken by the character | 0 |
| 34 | Bool | Bound | True if the item can't be traded | 0 | 
| 35 | Byte | Enchant | Added max life for the character | 0 |
| 36 | UInt32 | Data | Additional attributes for the item | 0 |
| 40 | Bool | Suspicious | Marked as suspicious for trading | 0 |
| 42 | Bool | Locked | Locked from being dropped or traded | 0 |
| 44 | Byte | [Color](#item-color) | Color modifier for the item | 3 |
| 48 | UInt32 | Owner ID | [Role ID](/network/identifiers.md) of the item owner | 1000000 |
| 52 | Char[16] | Owner Name | Owner's character name | Player |
| 68 | UInt32 | Hunter ID | [Role ID](/network/identifiers.md) of the hunter | 1000001 |
| 72 | Char[16] | Hunter Name | Hunter's character name | Hunter |
| 88 | UInt32 | Capture Date | Date string in the format YYYYMMDD | 20161001 |
| 96 | UInt32 | CPs | Cost for claiming | 1950 |
| 100 | Bool | Expired | True if the detain window has expired | 1 |
| 108 | UInt32 | Days | Days remaining to detain | 6 |