# MsgSynpOffer

This message is sent to the game client to list and update donations currently made to a guild / syndicate.

## Table of Contents

* [Patch 5615](#patch-5615)

## Patch 5615

#### Message Definition

✅ Verified (Client)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 84 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1058 |
| 4  | UInt32 | [SynpOfferUpdateFlags](#synpoffer-update-flags) | Which donations to update | 0 |
| 8  | Int32 | Money | Amount of money donated / debted | 0 |
| 12 | Int32 | EMoney | Amount of CPs donated / debted | 0 |
| 16 | UInt32 | Education | Amount of education points | 0 |
| 20 | UInt32 | Exploits | Amount of PK merit | 0 |
| 24 | UInt32 | Arsenal | Points in the arsenal | 0 |
| 28 | UInt32 | Roses | Flower points from roses | 0 |
| 32 | UInt32 | Orchids | Flower points from orchids | 0 |
| 36 | UInt32 | Lilies | Flower points from lilies | 0 |
| 40 | UInt32 | Tulips | Flower points from tulips | 0 |
| 44 | UInt32 | Faction | Amount of merit from faction PK | 0 |

#### SynpOffer Update Flags

✅ Verified (Client)

```proto
enum SynpOfferUpdateFlags {

    NONE = 0;
    MONEY = 1U << 0;
    EMONEY = 1U << 1;
    EDUCATION = 1U << 2;
    EXPLOIT = 1U << 3;
    ARSENAL = 1U << 4;
    ROSE = 1U << 5;
    ORCHID = 1U << 6;
    LILY = 1U << 7;
    TULIP = 1U << 8;
    FACTION_PK_MERIT = 1U << 9;
}
```