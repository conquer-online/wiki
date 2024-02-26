# MsgTrade

This message is sent by the client to request and manage a trade with another player.

When adding an item to the trade window, the server will receive a request to offer an item for trade and then respond by sending [MsgItemInfo](msgiteminfo.md) to show the item to the target player.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5017](#patch-5017)
* [Patch 5022](#patch-5022)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0 | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 12 |
| 2 | UInt16 | [MsgType](index.md#message-header) | Type of message | 1056 |
| 4 | UInt32 | Data | Data or a [unique Identifier](/network/identifiers.md) | 10 |
| 8 | UInt16 | [Action Type](#action-type) | The type of trade message | 6 |

#### Action Type

☑️ Assumed (Observed) - CoFuture + Soul

| Val | Name | Description | Recipient | Data |
|:------|:--------|:--------|:--------|:--------|
| 1  | APPLY | Request trade | Both | Requester's [Hero ID](/network/identifiers.md) |
| 2  | QUIT | Request cancel | Server | |
| 3  | OPEN | Open trade window | Client | Target's [Hero ID](/network/identifiers.md) |
| 4  | SUCCESS | Successful trade | Client | |
| 5  | FALSE | Failed trade | Client | |
| 6  | ADDITEM | Add item to trade window | Server | [Item ID](/network/identifiers.md) |
| 7  | ADDMONEY | Add money to trade window | Server | Money |
| 8  | PLAYERTOTALMONEY | Total money traded by target | Client | Money |
| 9  | HEROTOTALMONEY | Total money traded by hero | Client | Money |
| 10 | OK | Confirm trade | Both | |
| 11 | ADDITEM_FALSE | Cannot add item for trade | Client | [Item ID](/network/identifiers.md) |

## Patch 5017

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0 | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 12 |
| 2 | UInt16 | [MsgType](index.md#message-header) | Type of message | 1056 |
| 4 | UInt32 | Data | Data or a [unique Identifier](/network/identifiers.md) | 10 |
| 8 | UInt16 | [Action Type](#action-type) | The type of trade message | 6 |

#### Action Type

❓ Unverified

| Val | Name | Description | Recipient | Data |
|:------|:--------|:--------|:--------|:--------|
| 1  | APPLY | Request trade | Both | Requester's [Hero ID](/network/identifiers.md) |
| 2  | QUIT | Request cancel | Server | |
| 3  | OPEN | Open trade window | Client | Target's [Hero ID](/network/identifiers.md) |
| 4  | SUCCESS | Successful trade | Client | |
| 5  | FALSE | Failed trade | Client | |
| 6  | ADDITEM | Add item to trade window | Server | [Item ID](/network/identifiers.md) |
| 7  | ADDMONEY | Add money to trade window | Server | Money |
| 8  | PLAYERTOTALMONEY | Total money traded by target | Client | Money |
| 9  | HEROTOTALMONEY | Total money traded by hero | Client | Money |
| 10 | OK | Confirm trade | Both | |
| 11 | ADDITEM_FALSE | Cannot add item for trade | Client | [Item ID](/network/identifiers.md) |
| 12 | PLAYERTOTALEMONEY | Total CPs traded by target | Client | CPs |
| 13 | ADDEMONEY | Add CPs to trade window | Server | CPs |
| 14 | HEROTOTALEMONEY | Total CPs traded by hero | Client | CPs |

## Patch 5022

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0 | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 12 |
| 2 | UInt16 | [MsgType](index.md#message-header) | Type of message | 1056 |
| 4 | UInt32 | Data | Data or a [unique Identifier](/network/identifiers.md) | 10 |
| 8 | UInt16 | [Action Type](#action-type) | The type of trade message | 6 |

#### Action Type

❓ Unverified

| Val | Name | Description | Recipient | Data |
|:------|:--------|:--------|:--------|:--------|
| 1  | APPLY | Request trade | Both | Requester's [Hero ID](/network/identifiers.md) |
| 2  | QUIT | Request cancel | Server | |
| 3  | OPEN | Open trade window | Client | Target's [Hero ID](/network/identifiers.md) |
| 4  | SUCCESS | Successful trade | Client | |
| 5  | FALSE | Failed trade | Client | |
| 6  | ADDITEM | Add item to trade window | Server | [Item ID](/network/identifiers.md) |
| 7  | ADDMONEY | Add money to trade window | Server | Money |
| 8  | PLAYERTOTALMONEY | Total money traded by target | Client | Money |
| 9  | HEROTOTALMONEY | Total money traded by hero | Client | Money |
| 10 | OK | Confirm trade | Both | |
| 11 | ADDITEM_FALSE | Cannot add item for trade | Client | [Item ID](/network/identifiers.md) |
| 12 | PLAYERTOTALEMONEY | Total CPs traded by target | Client | CPs |
| 13 | ADDEMONEY | Add CPs to trade window | Server | CPs |
| 14 | HEROTOTALEMONEY | Total CPs traded by hero | Client | CPs |
| 15 | SUSPICIOUS_PROMPT | Prompt hero before confirm | Client | |
| 16 | SUSPICIOUS_OK | Confirm suspicious trade | Server | |