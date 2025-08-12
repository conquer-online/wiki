# MsgFamily

This message is received by the game server or game client as an action for managing a clan. It allows a clan leader to manage allies and enemies, and for family members to query for clan information.

## Table of Contents

* [Patch 5187](#patch-5187)

## Patch 5187

#### Message Definition

❗ Incomplete

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 88 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1312 |
| 4  | UInt32 | [Action](#clan-action-type) | How the message will be processed | 29 |
| 8  | UInt32 | [Target ID](../identifiers.md) | Unique identifier for the character or clan | 1000000 |
| 16 | UInt32 | [NetStringPacker](../stringpacker.md) | Strings | 5 10 FamilyName 8 UserName 18 FamilyOccupyString 18 FamilyDominatedMap  19 FamilyChallengedMap |

Alternative:

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 88 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1312 |
| 4  | UInt32 | [Action](#clan-action-type) | How the message will be processed | 29 |
| 8  | UInt32 | [Target ID](../identifiers.md) | Unique identifier for the character or clan | 1000000 |
| 16 | UInt32 | | | |

#### Clan Action Type

❗ Incomplete

🔶 Response data

| Val | Name | Description | Recipient | NetStringPacker |
|:------|:--------|:--------|:--------|:--------|
| 1  | QUERY |  |  |  | |
| 4  | QUERY_MEMBERS |  |  |  | |
| 9  | RECRUIT |  |  |  | |
| 10 | ACCEPT_RECRUIT |  |  |  | |
| 11 | JOIN |  |  |  | |
| 12 | ACCEPT_JOIN |  |  |  | |
| 13 | SHOW_ENEMY |  |  |  | |
| 14 | ADD_ENEMY |  |  |  | |
| 15 | DEL_ENEMY |  |  |  | |
| 16 | SHOW_ALLY |  |  |  | |
| 17 | ADD_ALLY |  |  |  | |
| 18 | ACCEPT_ALLY |  |  |  | |
| 20 | DEL_ALLY |  |  |  | |
| 21 | ABDICATE |  |  |  | |
| 22 | KICK_MEMBER |  |  |  | |
| 23 | QUIT |  |  |  | |
| 24 | SHOW_ANNOUNCE |  |  |  | |
| 25 | SET_ANNOUNCE |  |  |  | |
| 26 | DEDICATE |  |  |  | |
| 29 | QUERY_OCCUPY |  |  |  | |
