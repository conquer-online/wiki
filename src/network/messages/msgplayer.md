# MsgPlayer

This message is received by the client to spawn an entity on screen. Though the official name of the message suggests it spawns only players, it also spawns monsters on the game map. Entities must be less than or equal to 18 tiles away in both the x and y direction; otherwise, entities outside of that range will not spawn and automatically be cleaned up by the client.

In patches 5200 and above, this message is not enough to spawn equipment on the player. [MsgPlayerAttribInfo](msgplayerattribinfo.md) must be sent afterwards to finish spawning equipment and calculate final attributes.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5103](#patch-5103)

## Patch 4267

#### Player Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 65 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1014 |
| 4  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the entity | 1000000 |
| 8  | UInt32 | [Look Face](../../constants/lookface.md) | Mesh of the entity | 501002 |
| 12 | UInt32 | [Status Effect](../../files/content/statuseffect.ini.md) | Status effect bitmap | 0 |
| 16 | UInt32 | Syn Mask | SynID << 4 \| SynRank & 0x00FFFFFF | 0 |
| 20 | UInt32 | Garment | Garment's [item type](../../files/content/itemtype.dat.md) identifier | 0 |
| 24 | UInt32 | Armet | Headgear's [item type](../../files/content/itemtype.dat.md) identifier | 0 |
| 28 | UInt32 | Armor | Armor's [item type](../../files/content/itemtype.dat.md) identifier | 0 |
| 32 | UInt32 | Right Hand | Weapon's [item type](../../files/content/itemtype.dat.md) identifier | 0 |
| 36 | UInt32 | Left Hand | Weapon's [item type](../../files/content/itemtype.dat.md) identifier | 0 |
| 44 | UInt16 | X | X coordinate of the entity | 320 |
| 46 | UInt16 | Y | Y coordinate of the entity | 460 |
| 48 | UInt16 | Hair | Hairstyle and hair color	| 535 |
| 50 | Byte | [Direction](../../algorithms/calculations/direction.md) | Entity direction | 0 |
| 51 | Byte | Pose | Player's current pose | 100 |
| 52 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Name of the player | Player |
| Mate | Name of the player's spouse | Mate |

#### Monster Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 61 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1014 |
| 4  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the entity | 400001 |
| 8  | UInt32 | [Look Face](../../constants/lookface.md) | Mesh of the entity | 102 |
| 12 | UInt32 | [Status Effect](../../files/content/statuseffect.ini.md) | Status effect bitmap | 0 |
| 16 | UInt32 | Owner ID | [Identifier](../identifiers.md) of the pet's owner | 0 |
| 40 | UInt16 | Life | Hitpoints of the entity | 12 |
| 42 | UInt16 | Level | Level of the entity | 1 |
| 44 | UInt16 | X | X coordinate of the entity | 320 |
| 46 | UInt16 | Y | Y coordinate of the entity | 460 |
| 50 | Byte | [Direction](../../algorithms/calculations/direction.md) | Entity direction | 0 |
| 51 | Byte | Pose | Player's current pose | 100 |
| 52 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Name of the monster | Monster |

## Patch 5103

#### Player Message Definition

❓ Unverified - Imported from legacy wiki

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 107 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1014 |
| 4  | UInt32 | [Look Face](../../constants/lookface.md) | Mesh of the entity | 501002 |
| 8  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the entity | 1000000 |
| 12 | UInt32 | Syn Mask | SynID << 4 \| SynRank & 0x00FFFFFF | 0 |
| 16 | UInt64 | [Status Effect](../../files/content/statuseffect.ini.md) | Status effect bitmap | 0 |
| 24 | UInt32 | Garment | Garment's [item type](../../files/content/itemtype.dat.md) identifier | 0 |
| 28 | UInt32 | Armet | Headgear's [item type](../../files/content/itemtype.dat.md) identifier | 0 |
| 32 | UInt32 | Armor | Armor's [item type](../../files/content/itemtype.dat.md) identifier | 0 |
| 36 | UInt32 | Right Hand | Weapon's [item type](../../files/content/itemtype.dat.md) identifier | 0 |
| 40 | UInt32 | Left Hand | Weapon's [item type](../../files/content/itemtype.dat.md) identifier | 0 |
| 52 | UInt16 | Hair | Hairstyle and hair color	| 535 |
| 54 | UInt16 | X | X coordinate of the entity | 320 |
| 56 | UInt16 | Y | Y coordinate of the entity | 460 |
| 58 | Byte | [Direction](../../algorithms/calculations/direction.md) | Entity direction | 0 |
| 59 | Byte | Pose | Player's current pose | 100 |
| 60 | UInt16 | Metempsychosis | Metempsychosis level | 0 |
| 70 | UInt16 | Shared BP | Battle power from mentor | 0 |
| 77 | UInt32 | Flower Rank | Flower ranking | 0 |
| 81 | UInt32 | Nobility Rank | Nobility ranking | 12 |
| 85 | UInt16 | Armor Color | Color of equipped armor | 3 |
| 87 | UInt16 | Shield Color | Color of equipped shield | 4 |
| 89 | UInt16 | Armet Color | Color of equipped headgear | 3 |
| 91 | UInt32 | Study Points | Quiz show points | 6546 |
| 95 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Name of the player | Player |
| Mate | Name of the player's spouse | Mate |

#### Monster Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 103 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 10014 |
| 4  | UInt32 | [Look Face](../../constants/lookface.md) | Mesh of the entity | 501002 |
| 8  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the entity | 1000000 |
| 12 | UInt32 | Owner ID | [Identifier](../identifiers.md) of the pet's owner | 0 |
| 16 | UInt64 | [Status Effect](../../files/content/statuseffect.ini.md) | Status effect bitmap | 0 |
| 48 | UInt16 | Life | Hitpoints of the entity | 12 |
| 54 | UInt16 | X | X coordinate of the entity | 320 |
| 56 | UInt16 | Y | Y coordinate of the entity | 460 |
| 58 | Byte | [Direction](../../algorithms/calculations/direction.md) | Entity direction | 0 |
| 59 | Byte | Pose | Player's current pose | 100 |
| 62 | UInt16 | Level | Level of the entity | 1 |
| 95 | [NetStringPacker](../stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Name | Name of the monster | Monster |
