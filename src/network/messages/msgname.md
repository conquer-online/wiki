# MsgName

This message allows the client to query for a string update, and allows the game server to trigger a string command on the client. In later versions of the client, the purpose of this message is mostly superseded by [MsgAction](msgaction.md), which adds an optional string parameter. Even in lower patches, a few types are unimplemented since they overlap with functionality in other messages, such as deleting the role.

Fireworks are an interesting type in this packet, as the way the client processes a fireworks request is to make the string an even number of letters, iterate through every two characters, and spawn a firework at a random coordinate near the center of the screen for those two characters.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5017](#patch-5017)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 10 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1015 |
| 4  | UInt32 | Data | A parameter, target [role ID](../identifiers.md), or coordinates | 1000001 |
| 8  | Byte | [Action Type](#action-type) | The type of contents in the message | 6 |
| 9 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### Action Type

☑️ Assumed (Observed) - CoFuture + Soul

🔶 Response data

| Val | Name | Description | Recipient | Data | NetStringPacker |
|:------|:--------|:--------|:--------|:--------|:--------|
| 1  | FIREWORKS | Spawn fireworks | Client | [Hero ID](../identifiers.md) | 1 4 Test |
| 3  | CHANGE_SYN | Update guild name | Client | [Guild ID](../identifiers.md) | 1 4 Name |
| 6  | MATE | Update mate | Client | [Hero ID](../identifiers.md) | 1 4 Mate |
| 9  | MAP_EFFECT | Spawn effect at coordinates | Client | `LOW:` X `HIGH:` Y | 1 7 rainbow |
| 10 | ROLE_EFFECT | Spawn effect on role | Client | [Role ID](../identifiers.md) | 1 9 warrior-s |
| 11 | MEMBER_LIST | Get guild member list | Server | Index | 1 6 Member 🔶 |
| 16 | QUERY_MATE | Get mate's name | Server | [Hero ID](../identifiers.md) | 1 4 Mate 🔶 |
| 17 | ADD_DICE_PLAYER | Add player / open game | Server | Dice Game ID 🔶 | 1 6 Player |
| 18 | DEL_DICE_PLAYER | Delete player / close game | Server | Dice Game ID | 1 6 Player |
| 19 | DICE_BONUS | Update money bonus | Client | Money | 1 6 Player |
| 20 | PLAYER_WAVE | Play DX Sound | Client | `LOW:` X `HIGH:` Y | 1 11 sound/1.wav |

## Patch 5017

#### Message Definition

☑️ Assumed (Observed) - CoFuture

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 10 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1015 |
| 4  | UInt32 | Data | A parameter, target [role ID](../identifiers.md), or coordinates | 1000001 |
| 8  | Byte | [Action Type](#action-type-1) | The type of contents in the message | 6 |
| 9 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### Action Type

☑️ Assumed (Observed) - CoFuture + Soul

🔶 Response data

| Val | Name | Description | Recipient | Data | NetStringPacker |
|:------|:--------|:--------|:--------|:--------|:--------|
| 1  | FIREWORKS | Spawn fireworks | Client | [Hero ID](../identifiers.md) | 1 4 Test |
| 3  | CHANGE_SYN | Update guild name | Client | [Guild ID](../identifiers.md) | 1 4 Name |
| 6  | MATE | Update mate | Client | [Hero ID](../identifiers.md) | 1 4 Mate |
| 9  | MAP_EFFECT | Spawn effect at coordinates | Client | `LOW:` X `HIGH:` Y | 1 7 rainbow |
| 10 | ROLE_EFFECT | Spawn effect on role | Client | [Role ID](../identifiers.md) | 1 9 warrior-s |
| 11 | MEMBER_LIST | Get guild member list | Server | Index | 1 6 Member 🔶 |
| 16 | QUERY_MATE | Get mate's name | Server | [Hero ID](../identifiers.md) | 1 4 Mate 🔶 |
| 17 | ADD_DICE_PLAYER | Add player / open game | Server | Dice Game ID 🔶 | 1 6 Player |
| 18 | DEL_DICE_PLAYER | Delete player / close game | Server | Dice Game ID | 1 6 Player |
| 19 | DICE_BONUS | Update money bonus | Client | Money | 1 6 Player |
| 20 | PLAYER_WAVE | Play DX Sound | Client | `LOW:` X `HIGH:` Y | 1 11 sound/1.wav |
| 26 | WHISPER_DIALOG | Dialog window details | Server |  | See [below](#whisper-netstringpacker-fields) 🔶 |

#### Whisper NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Target player | Player |
| Details | HeroID Level Potency GuildName | 1000001 1 1 Guild |