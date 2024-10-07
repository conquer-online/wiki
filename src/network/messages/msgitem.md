# MsgItem

This message is received by the game server as a client request to use or act on an item. Item actions can be buying, selling, equipping, repairing, dropping, upgrading, and more. A miscellaneous function of this message is as a ping response. The client sends this message once every 10 seconds to show the latency to the server in the client.

The message can also be sent to the client for specific actions such as force unequipping, force dropping, updating the durability of an item, or updating the amount of an item.

> ⚠️ __WARNING__
>
> Ensure that the item type for item improvements matches the consumption item type when improving items. If composing two items together, ensure that the fuel item is also different than the improved item. In all cases, location should also be validated (you cannot upgrade an item from any distance or from any map, same with vending items at player booths). If showing an item, generate a new sharing identifier rather than exposing the item's unique identifier.  

## Requests

Requests can be of multiple sizes, not necessarily always containing an amount or additional fields past the system time. When processing these request messages, this should be taken into account so not to use fields that have been unspecified.

## Responses

Most item actions are initiated by the player. Each request expects a response of either MsgItem (this message) with a filled data field, or a [MsgItemInfo](msgiteminfo.md) of the resulting item (like from a shop purchase).

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5017](#patch-5017)
* [Patch 5517](#patch-5517)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 20 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1009 |
| 4  | UInt32 | [ID](../identifiers.md) | Unique identifier for the item or role | 1000000 |
| 8  | UInt32 | Data | Payload usually of the item type or position | 730001 |
| 12 | UInt32 | [Action](#item-action) | How to processes the message | 2 |
| 16 | UInt32 | [System Time](../timestamp.md) | Milliseconds of system uptime | 1579535985 |

#### Item Action

☑️ Assumed (Observed) - CoFuture + Soul

🔶 Response data

| Val | Name | Description | Recipient | ID | Data |
|:------|:--------|:--------|:--------|:--------|:--------|
| 1 | BUY | Purchase from shop | Server | [NPC](../identifiers.md) | [Item Type](../../files/content/itemtype.dat.md) |
| 2 | SELL | Sell to shop | Server | [NPC](../identifiers.md) | [Item ID](../identifiers.md) |
| 3 | DROP | Drops an item or removes it | Server | [Item](../identifiers.md) | `LOW:` X `HIGH:` Y 🔶 |
| 4 | EQUIP | Equip to position on body | Server | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 5 | UPDATE | Updates an item | Client | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 6 | UNEQUIP | Force unequip | Client | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 8 | COMBINE | Combine two of same type | Server | [Item](../identifiers.md) | [Item ID](../identifiers.md) |
| 9 | QUERY_MONEY | Request warehouse money | Server | [NPC](../identifiers.md) | Money 🔶 |
| 10 | SAVE_MONEY | Deposit warehouse money | Server | [NPC](../identifiers.md) | Money |
| 11 | DRAW_MONEY | Withdraw warehouse money | Server | [NPC](../identifiers.md) | Money |
| 12 | DROP_MONEY | Drop money on the floor | Server | Money | `LOW:` X `HIGH:` Y |
| 14 | REPAIR | Repair [durability](../../algorithms/calculations/item-durability.md) | Server | [Item](../identifiers.md) | |
| 17 | DURABILITY | Update [durability](../../algorithms/calculations/item-durability.md) | Client | [Position](msgiteminfo.md#item-position) | [Durability](../../algorithms/calculations/item-durability.md) |
| 18 | DROP_EQUIPMENT | Force delete equipment | Client | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 19 | IMPROVE | Quality upgrade | Server | [Item](../identifiers.md) | Dragonball [Item ID](../identifiers.md) |
| 20 | UPLEV | Level upgrade | Server | [Item](../identifiers.md) | Meteor [Item ID](../identifiers.md) |
| 21 | BOOTH_QUERY | Show booth item | Server | [Item](../identifiers.md) | |
| 22 | BOOTH_ADD | Add to booth | Server | [Item](../identifiers.md) | Money |
| 23 | BOOTH_DEL | Remove from booth | Server | [Item](../identifiers.md) | [Shop](../identifiers.md) |
| 24 | BOOTH_BUY | Buy from a booth | Server | [Item](../identifiers.md) | [Shop](../identifiers.md) |
| 27 | PING | Latency check | Server | [Player](../identifiers.md) | |

## Patch 5017

#### Message Definition

☑️ Assumed (Observed) - ApexConquer

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 24 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1009 |
| 4  | UInt32 | [ID](../identifiers.md) | Unique identifier for the item or role | 1000000 |
| 8  | UInt32 | Data | Payload usually of the item type or position | 730001 |
| 12 | UInt32 | [Action](#item-action-1) | How the server processes the message | 2 |
| 16 | UInt32 | [System Time](../timestamp.md) | Milliseconds of system uptime | 1579535985 |
| 20 | UInt32 | Amount | Amount of items being purchased or used | 0 |

#### Item Action

☑️ Assumed (Observed) - ApexConquer

🔶 Response data

| Val | Name | Description | Recipient | ID | Data |
|:------|:--------|:--------|:--------|:--------|:--------|
| 1 | BUY | Purchase from shop | Server | [NPC](../identifiers.md) | [Item Type](../../files/content/itemtype.dat.md) |
| 2 | SELL | Sell to shop | Server | [NPC](../identifiers.md) | [Item ID](../identifiers.md) |
| 3 | DROP | Drops an item or removes it | Server | [Item](../identifiers.md) | `LOW:` X `HIGH:` Y 🔶 |
| 4 | EQUIP | Equip to position on body | Server | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 5 | UPDATE | Updates an item | Client | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 6 | UNEQUIP | Force unequip | Client | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 8 | COMBINE | Combine two of same type | Server | [Item](../identifiers.md) | [Item ID](../identifiers.md) |
| 9 | QUERY_MONEY | Request warehouse money | Server | [NPC](../identifiers.md) | Money 🔶 |
| 10 | SAVE_MONEY | Deposit warehouse money | Server | [NPC](../identifiers.md) | Money |
| 11 | DRAW_MONEY | Withdraw warehouse money | Server | [NPC](../identifiers.md) | Money |
| 12 | DROP_MONEY | Drop money on the floor | Server | Money | `LOW:` X `HIGH:` Y |
| 14 | REPAIR | Repair [durability](../../algorithms/calculations/item-durability.md) | Server | [Item](../identifiers.md) | |
| 17 | DURABILITY | Update [durability](../../algorithms/calculations/item-durability.md) | Client | [Position](msgiteminfo.md#item-position) | [Durability](../../algorithms/calculations/item-durability.md) |
| 18 | DROP_EQUIPMENT | Force delete equipment | Client | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 19 | IMPROVE | Quality upgrade | Server | [Item](../identifiers.md) | Dragonball [Item ID](../identifiers.md) |
| 20 | UPLEV | Level upgrade | Server | [Item](../identifiers.md) | Meteor [Item ID](../identifiers.md) |
| 21 | BOOTH_QUERY | Show booth item | Server | [Item](../identifiers.md) | |
| 22 | BOOTH_ADD | Add to booth | Server | [Item](../identifiers.md) | Money |
| 23 | BOOTH_DEL | Remove from booth | Server | [Item](../identifiers.md) | [Shop](../identifiers.md) |
| 24 | BOOTH_BUY | Buy from a booth | Server | [Item](../identifiers.md) | [Shop](../identifiers.md) |
| 27 | PING | Latency check | Server | [Player](../identifiers.md) | |
| 28 | ENCHANT | Enchant item | Server | [Item](../identifiers.md) | Gem [Item ID](../identifiers.md) |
| 29 | BOOTH_ADD_EMONEY | Add EMoney to booth | Server | [Item](../identifiers.md) | EMoney |

## Patch 5517

#### Message Definition

☑️ Assumed (Observed) - ApexConquer

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 60 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1009 |
| 4  | UInt32 | [ID](../identifiers.md) | Unique identifier for the item or role | 1000000 |
| 8  | UInt32 | Data | Payload usually of the item type or position | 730001 |
| 12 | UInt32 | [Action](#item-action-2) | How the server processes the message | 2 |
| 16 | UInt32 | [System Time](../timestamp.md) | Milliseconds of system uptime | 1579535985 |
| 20 | UInt32 | Amount | Amount of items being purchased or used | 0 |
| 24 | UInt32[9] | Equipment | Equipment in order of slot position | 0 |

#### Item Action

☑️ Assumed (Observed) - ConquerServerV3

🔶 Response data

| Val | Name | Description | Recipient | ID | Data |
|:------|:--------|:--------|:--------|:--------|:--------|
| 1 | BUY | Purchase from shop | Server | [NPC](../identifiers.md) | [Item Type](../../files/content/itemtype.dat.md) |
| 2 | SELL | Sell to shop | Server | [NPC](../identifiers.md) | [Item ID](../identifiers.md) |
| 4 | EQUIP | Equip to position on body | Server | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 5 | UPDATE | Updates an item | Client | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 6 | UNEQUIP | Force unequip | Client | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 9 | QUERY_MONEY | Request warehouse money | Server | [NPC](../identifiers.md) | Money 🔶 |
| 10 | SAVE_MONEY | Deposit warehouse money | Server | [NPC](../identifiers.md) | Money |
| 11 | DRAW_MONEY | Withdraw warehouse money | Server | [NPC](../identifiers.md) | Money |
| 14 | REPAIR | Repair [durability](../../algorithms/calculations/item-durability.md) | Server | [Item](../identifiers.md) | |
| 17 | DURABILITY | Update [durability](../../algorithms/calculations/item-durability.md) | Client | [Position](msgiteminfo.md#item-position) | [Durability](../../algorithms/calculations/item-durability.md) |
| 18 | DROP_EQUIPMENT | Force delete equipment | Client | [Item](../identifiers.md) | [Position](msgiteminfo.md#item-position) |
| 19 | IMPROVE | Quality upgrade | Server | [Item](../identifiers.md) | Dragonball [Item ID](../identifiers.md) |
| 20 | UPLEV | Level upgrade | Server | [Item](../identifiers.md) | Meteor [Item ID](../identifiers.md) |
| 21 | BOOTH_QUERY | Show booth item | Server | [Item](../identifiers.md) | |
| 22 | BOOTH_ADD | Add to booth | Server | [Item](../identifiers.md) | Money |
| 23 | BOOTH_DEL | Remove from booth | Server | [Item](../identifiers.md) | [Shop](../identifiers.md) |
| 24 | BOOTH_BUY | Buy from a booth | Server | [Item](../identifiers.md) | [Shop](../identifiers.md) |
| 27 | PING | Latency check | Server | [Hero](../identifiers.md) | |
| 28 | ENCHANT | Enchant item | Server | [Item](../identifiers.md) | Gem [Item ID](../identifiers.md) |
| 29 | BOOTH_ADD_EMONEY | Add EMoney to booth | Server | [Item](../identifiers.md) | EMoney |
| 33 | DETAIN_REDEEM | Redeem a detained item | Server | [Item](../identifiers.md) | |
| 35 | SOCKET | Socket a talisman | Server | [Item](../identifiers.md) | [Item ID](../identifiers.md) |
| 36 | SOCKET_EMONEY | Socket talisman with EMoney | Server | [Item](../identifiers.md) | EMoney |
| 37 | DROP | Drops an item or removes it | Server | [Item](../identifiers.md) | |
| 38 | DROP_MONEY | Drop money on the floor | Server | Money | |
| 40 | UPBLESS | Upgrade bless | Server | [Item](../identifiers.md) | |
| 41 | SHOW_ACCESSORY | Show an accessory | Server | [Item](../identifiers.md) | |
| 46 | SHOW_EQUIPMENT | Response for MsgAction | Client | [Hero](../identifiers.md) | |
| 48 | COMBINE | Combine two of same type | Server | [Item](../identifiers.md) | [Item ID](../identifiers.md) |
| 49 | SPLIT | Split into two | Server | [Item](../identifiers.md) | |
| 52 | SHOW_ITEM | Item card | Client | [Item](../identifiers.md) | |