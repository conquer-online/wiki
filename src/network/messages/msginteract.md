# MsgInteract

This message is used to request an interaction with another player or broadcast an interaction to surrounding players. Some example interactions include physical and magical attacks, proposing, and killing a player. 

Magic attacks in Conquer Online are obfuscated using bit rotations and XORs. See the example below from Soul.

```c++
#define ENCODE_MAGICATTACK(idUser, usType, idTarget, usPosX, usPosY)                           \
{                                                                                              \
    usType = (::ExchangeShortBits((usType - 0x14BE), 3) ^ (idUser) ^ 0x915D);                  \
    idTarget = ::ExchangeLongBits(((idTarget - 0x8B90B51A) ^ (idUser) ^ 0x5F2D2463), 32 - 13); \
    usPosX = (::ExchangeShortBits((usPosX - 0xDD12), 1) ^ (idUser) ^ 0x2ED6);                  \
    usPosY = (::ExchangeShortBits((usPosY - 0x76DE), 5) ^ (idUser) ^ 0xB99B);                  \
}

#define DECODE_MAGICATTACK(idUser, usType, idTarget, usPosX, usPosY)                          \
{                                                                                             \
    usType = 0xFFFF & (::ExchangeShortBits(((usType) ^ (idUser) ^ 0x915D), 16 - 3) + 0x14BE); \
    idTarget = (::ExchangeLongBits((idTarget), 13) ^ (idUser) ^ 0x5F2D2463) + 0x8B90B51A;     \
    usPosX = 0xFFFF & (::ExchangeShortBits(((usPosX) ^ (idUser) ^ 0x2ED6), 16 - 1) + 0xDD12); \
    usPosY = 0xFFFF & (::ExchangeShortBits(((usPosY) ^ (idUser) ^ 0xB99B), 16 - 5) + 0x76DE); \
}

inline unsigned int ExchangeShortBits(unsigned long nData, int nBits)
{
    MYASSERT(nBits >= 0 && nBits < 16);
    nData &= 0xFFFF;
    return ((nData >> nBits) | (nData << (16 - nBits))) & 0xFFFF;
}

inline unsigned int ExchangeLongBits(unsigned long nData, int nBits)
{
    MYASSERT(nBits >= 0 && nBits < 32);
    return (nData >> nBits) | (nData << (32 - nBits));
}
```

Similar to other messages, MsgInteract also contains types that overlap with other types in other messages. For example, aborting magic was handled in MsgInteract, but is instead duplicated and utilized in [MsgAction](msgaction.md).

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5017](#patch-5017)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1022 |
| 4  | UInt32 | [System Time](../timestamps.md) | Milliseconds of system uptime | 10000 |
| 8  | UInt32 | Sender | [Role ID](../identifiers.md) of the initiator | 1000000 |
| 12 | UInt32 | Target | [Role ID](../identifiers.md) of the target | 1000001 |
| 16 | UInt16 | X | X coordinate of the interaction | 320 |
| 18 | UInt16 | Y | Y coordinate of the interaction | 460 |
| 20 | UInt32 | [Type](#interaction-type) | How to processes the message | 14 |
| 24 | UInt32 | Data | Value associated with the interaction | 1 |

#### Interaction Type

☑️ Assumed (Observed) - CoFuture + Soul

🔶 Response data

| Val | Name | Description | Recipient | Data |
|:----|:--------|:--------|:--------|:--------|
| 2  | ATTACK | Physical attack | Server | Damage 🔶 |
| 8  | COURT  | Propose to a player | Server | |
| 9  | MARRY  | Accept a proposal | Server | |
| 14 | KILL | Confirms kill of an entity | Client | Count |
| 21 | MAGIC_ATTACK | [Magical attack](../../algorithms/calculations/damage.md) | Server | `HIGH:` MagicType |
| 23 | REFLECT_WEAPON | Reflect a [physical attack](../../algorithms/calculations/damage.md) | Client | Damage |
| 24 | BUMP | Bumped from dash | Client | Direction |
| 25 | SHOOT | Shoot projectile | Server | Damage 🔶 |
| 26 | REFLECT_MAGIC | Reflect a [magical attack](../../algorithms/calculations/damage.md) | Client | Damage |

## Patch 5017

#### Message Definition

☑️ Assumed (Observed) - COPSv6

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1022 |
| 4  | UInt32 | [System Time](../timestamps.md) | Milliseconds of system uptime | 10000 |
| 8  | UInt32 | Sender | [Role ID](../identifiers.md) of the initiator | 1000000 |
| 12 | UInt32 | Target | [Role ID](../identifiers.md) of the target | 1000001 |
| 16 | UInt16 | X | X coordinate of the interaction | 320 |
| 18 | UInt16 | Y | Y coordinate of the interaction | 460 |
| 20 | UInt32 | [Type](#interaction-type-1) | How to processes the message | 14 |
| 24 | UInt32 | Data | Value associated with the interaction | 1 |
| 28 | UInt32 | Progress | Progress on an interaction | 0 |

#### Interaction Type

☑️ Assumed (Observed) - COPSv6

🔶 Response data

| Val | Name | Description | Recipient | Data | Progress |
|:----|:--------|:--------|:--------|:--------|:--------|
| 2  | ATTACK | Physical attack | Server | Damage 🔶 | |
| 8  | COURT  | Propose to a player | Server | | |
| 9  | MARRY  | Accept a proposal | Server | | | 
| 14 | KILL | Confirms kill of an entity | Client | Count | |
| 21 | MAGIC_ATTACK | [Magical attack](../../algorithms/calculations/damage.md) | Server | `HIGH:` MagicType |
| 23 | REFLECT_WEAPON | Reflect a [physical attack](../../algorithms/calculations/damage.md) | Client | Damage |
| 24 | BUMP | Bumped from dash | Client | Direction | |
| 25 | SHOOT | Shoot projectile | Server | Damage 🔶 | |
| 26 | REFLECT_MAGIC | Reflect a [magical attack](../../algorithms/calculations/damage.md) | Client | Damage |
| 30 | JAR_PROGRESS | Cloud Saint Jar count | Server | 0 | Count 🔶 |
