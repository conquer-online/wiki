# MsgUserInfo

This message is sent to the game client from the game server to initialize the hero role with character data. It's expected to be sent after the game server processes [MsgConnect](msgconnect.md) after sending ANSWER_OK using [MsgTalk](msgtalk.md). In response to this message, the client will then send a [MsgAction](msgaction.md) message requesting the location of the character.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 4343](#patch-4343)
* [Patch 5017](#patch-5017)
* [Patch 5065](#patch-5065)
* [Patch 5095](#patch-5095)
* [Patch 5165](#patch-5165)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 73 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1006 |
| 4  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | UInt32 | [Look](../../algorithms/calculations/roleview.md) | Character view mesh | 501002 |
| 12 | UInt16 | [Hair](../../constants/hairstyles.md) | Hairstyle and hair color | 535 |
| 16 | UInt32 | Money | Earned virtual player currency in pocket | 10000 |
| 20 | UInt64 | Experience | Leveling experience | 1000 |
| 40 | UInt16 | [Strength](../../algorithms/calculations/attributes.md) | Physical attack power | 7 |
| 42 | UInt16 | [Agility](../../algorithms/calculations/attributes.md) | Physical accuracy | 2 |
| 44 | UInt16 | [Vitality](../../algorithms/calculations/attributes.md) | Health increase | 4 |
| 46 | UInt16 | [Spirit](../../algorithms/calculations/attributes.md) | Mana increase | 0 |
| 48 | UInt16 | [Attributes](../../algorithms/calculations/attributes.md) | Unspent attribute points | 0 |
| 50 | UInt16 | Life | Current health of the character | 99 |
| 52 | UInt16 | Mana | Current mana of the character | 0 |
| 54 | UInt16 | Pk | PK points from slaying other players | 0 |
| 56 | Byte | Level | Character level | 1 |
| 57 | Byte | [Profession](../../constants/heroprofession.md) | Current profession | 10 |
| 59 | Byte | Metempsychosis | Number of rebirths | 0 |
| 60 | Bool | AutoAllot | True to automatically allot attributes | 1 |
| 61 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Name of the character | Player |
| Mate | The character the player is married to | None |

## Patch 4343

#### Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 77 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1006 |
| 4  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | UInt32 | [Look](../../algorithms/calculations/roleview.md) | Character view mesh | 501002 |
| 12 | UInt16 | [Hair](../../constants/hairstyles.md) | Hairstyle and hair color | 535 |
| 14 | UInt32 | Money | Earned virtual player currency in pocket | 10000 |
| 18 | UInt32 | EMoney | Paid virtual player currency in pocket | 0 |
| 22 | UInt64 | Experience | Leveling experience | 1000 |
| 44 | UInt16 | [Strength](../../algorithms/calculations/attributes.md) | Physical attack power | 7 |
| 46 | UInt16 | [Agility](../../algorithms/calculations/attributes.md) | Physical accuracy | 2 |
| 48 | UInt16 | [Vitality](../../algorithms/calculations/attributes.md) | Health increase | 4 |
| 50 | UInt16 | [Spirit](../../algorithms/calculations/attributes.md) | Mana increase | 0 |
| 52 | UInt16 | [Attributes](../../algorithms/calculations/attributes.md) | Unspent attribute points | 0 |
| 54 | UInt16 | Life | Current health of the character | 99 |
| 56 | UInt16 | Mana | Current mana of the character | 0 |
| 58 | UInt16 | Pk | PK points from slaying other players | 0 |
| 60 | Byte | Level | Character level | 1 |
| 61 | Byte | [Profession](../../constants/heroprofession.md) | Current profession | 10 |
| 63 | Byte | Metempsychosis | Number of rebirths | 0 |
| 64 | Bool | AutoAllot | True to automatically allot attributes | 1 |
| 65 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Name of the character | Player |
| Mate | The character the player is married to | None |

## Patch 5017

#### Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 79 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1006 |
| 4  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | UInt32 | [Look](../../algorithms/calculations/roleview.md) | Character view mesh | 501002 |
| 12 | UInt16 | [Hair](../../constants/hairstyles.md) | Hairstyle and hair color | 535 |
| 14 | UInt32 | Money | Earned virtual player currency in pocket | 10000 |
| 18 | UInt32 | EMoney | Paid virtual player currency in pocket | 0 |
| 22 | UInt64 | Experience | Leveling experience | 1000 |
| 46 | UInt16 | [Strength](../../algorithms/calculations/attributes.md) | Physical attack power | 7 |
| 48 | UInt16 | [Agility](../../algorithms/calculations/attributes.md) | Physical accuracy | 2 |
| 50 | UInt16 | [Vitality](../../algorithms/calculations/attributes.md) | Health increase | 4 |
| 52 | UInt16 | [Spirit](../../algorithms/calculations/attributes.md) | Mana increase | 0 |
| 54 | UInt16 | [Attributes](../../algorithms/calculations/attributes.md) | Unspent attribute points | 0 |
| 56 | UInt16 | Life | Current health of the character | 99 |
| 58 | UInt16 | Mana | Current mana of the character | 0 |
| 60 | UInt16 | Pk | PK points from slaying other players | 0 |
| 62 | Byte | Level | Character level | 1 |
| 63 | Byte | [Profession](../../constants/heroprofession.md) | Current profession | 10 |
| 64 | Byte | [Previous Profession](../../constants/heroprofession.md) | Profession before latest rebirth | 0 |
| 65 | Byte | Metempsychosis | Number of rebirths | 0 |
| 66 | Bool | AutoAllot | True to automatically allot attributes | 1 |
| 67 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Name of the character | Player |
| Mate | The character the player is married to | None |

## Patch 5065

#### Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 83 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1006 |
| 4  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | UInt32 | [Look](../../algorithms/calculations/roleview.md) | Character view mesh | 501002 |
| 12 | UInt16 | [Hair](../../constants/hairstyles.md) | Hairstyle and hair color | 535 |
| 14 | UInt32 | Money | Earned virtual player currency in pocket | 10000 |
| 18 | UInt32 | EMoney | Paid virtual player currency in pocket | 0 |
| 22 | UInt64 | Experience | Leveling experience | 1000 |
| 50 | UInt16 | [Strength](../../algorithms/calculations/attributes.md) | Physical attack power | 7 |
| 52 | UInt16 | [Agility](../../algorithms/calculations/attributes.md) | Physical accuracy | 2 |
| 54 | UInt16 | [Vitality](../../algorithms/calculations/attributes.md) | Health increase | 4 |
| 56 | UInt16 | [Spirit](../../algorithms/calculations/attributes.md) | Mana increase | 0 |
| 58 | UInt16 | [Attributes](../../algorithms/calculations/attributes.md) | Unspent attribute points | 0 |
| 60 | UInt16 | Life | Current health of the character | 99 |
| 62 | UInt16 | Mana | Current mana of the character | 0 |
| 64 | UInt16 | Pk | PK points from slaying other players | 0 |
| 66 | Byte | Level | Character level | 1 |
| 67 | Byte | [Profession](../../constants/heroprofession.md) | Current profession | 10 |
| 68 | Byte | [Previous Profession](../../constants/heroprofession.md) | Profession before latest rebirth | 0 |
| 69 | Byte | Metempsychosis | Number of rebirths | 0 |
| 70 | Bool | AutoAllot | True to automatically allot attributes | 1 |
| 71 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Name of the character | Player |
| Mate | The character the player is married to | None |

## Patch 5095

#### Message Definition

☑️ Assumed (Observed) - CoEmu

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 91 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1006 |
| 4  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | UInt32 | [Look](../../algorithms/calculations/roleview.md) | Character view mesh | 501002 |
| 12 | UInt16 | [Hair](../../constants/hairstyles.md) | Hairstyle and hair color | 535 |
| 14 | UInt32 | Money | Earned virtual player currency in pocket | 10000 |
| 18 | UInt32 | EMoney | Paid virtual player currency in pocket | 0 |
| 22 | UInt64 | Experience | Leveling experience | 1000 |
| 54 | UInt16 | [Strength](../../algorithms/calculations/attributes.md) | Physical attack power | 7 |
| 56 | UInt16 | [Agility](../../algorithms/calculations/attributes.md) | Physical accuracy | 2 |
| 58 | UInt16 | [Vitality](../../algorithms/calculations/attributes.md) | Health increase | 4 |
| 60 | UInt16 | [Spirit](../../algorithms/calculations/attributes.md) | Mana increase | 0 |
| 62 | UInt16 | [Attributes](../../algorithms/calculations/attributes.md) | Unspent attribute points | 0 |
| 64 | UInt16 | Life | Current health of the character | 99 |
| 66 | UInt16 | Mana | Current mana of the character | 0 |
| 68 | UInt16 | Pk | PK points from slaying other players | 0 |
| 70 | Byte | Level | Character level | 1 |
| 71 | Byte | [Profession](../../constants/heroprofession.md) | Current profession | 10 |
| 72 | Byte | [Previous Profession](../../constants/heroprofession.md) | Profession before latest rebirth | 0 |
| 73 | Byte | Metempsychosis | Number of rebirths | 0 |
| 74 | Bool | AutoAllot | True to automatically allot attributes | 1 |
| 75 | UInt32 | Quiz Points | Total quiz points | 0 |
| 79 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Name of the character | Player |
| Mate | The character the player is married to | None |

## Patch 5165

#### Message Definition

❓ Unverified - Assumed from Impulse + Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 99 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1006 |
| 4  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | UInt32 | [Look](../../algorithms/calculations/roleview.md) | Character view mesh | 501002 |
| 12 | UInt16 | [Hair](../../constants/hairstyles.md) | Hairstyle and hair color | 535 |
| 14 | UInt32 | Money | Earned virtual player currency in pocket | 10000 |
| 18 | UInt32 | EMoney | Paid virtual player currency in pocket | 0 |
| 22 | UInt64 | Experience | Leveling experience | 1000 |
| 50 | UInt16 | [Strength](../../algorithms/calculations/attributes.md) | Physical attack power | 7 |
| 52 | UInt16 | [Agility](../../algorithms/calculations/attributes.md) | Physical accuracy | 2 |
| 54 | UInt16 | [Vitality](../../algorithms/calculations/attributes.md) | Health increase | 4 |
| 56 | UInt16 | [Spirit](../../algorithms/calculations/attributes.md) | Mana increase | 0 |
| 58 | UInt16 | [Attributes](../../algorithms/calculations/attributes.md) | Unspent attribute points | 0 |
| 60 | UInt16 | Life | Current health of the character | 99 |
| 62 | UInt16 | Mana | Current mana of the character | 0 |
| 64 | UInt16 | Pk | PK points from slaying other players | 0 |
| 66 | Byte | Level | Character level | 1 |
| 67 | Byte | [Profession](../../constants/heroprofession.md) | Current profession | 10 |
| 68 | Byte | [Previous Profession](../../constants/heroprofession.md) | Profession before latest rebirth | 0 |
| 69 | Byte | Metempsychosis | Number of rebirths | 0 |
| 68 | Byte | [First Profession](../../constants/heroprofession.md) | Profession before first rebirth (if on second) | 0 |
| 70 | Bool | AutoAllot | True to automatically allot attributes | 1 |
| 71 | UInt32 | Quiz Points | Total quiz points | 0 |
| 75 | UInt16 | Enlighten Points | [Enlightenment](../../algorithms/calculations/enlightenment.md) points progress | 0 |
| 77 | UInt16 | Enlighten Exp | [Enlightenment](../../algorithms/calculations/enlightenment.md) experience | 0 |
| 87 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Name of the character | Player |
| Mate | The character the player is married to | None |
