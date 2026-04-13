# Gem

Gems can be socketed into equipment to grant bonuses. Equipment can have up to two socket slots, each holding one gem.

Gems come in three quality grades: Normal, Refined, and Super.

## Table of Contents

* [Patch 5517](#patch-5517)

## Patch 5517

### Gem Item IDs

Gem item IDs fall in the range [`700000–709999`](itemid.md#overall-item-id-ranges), identified by the client via `CItem::IsGem`. The last digit of the ID encodes the [Gems Quality](itemid.md#gems-quality).

| Digit | Quality |
|:------|:--------|
| 1     | Normal  |
| 2     | Refined |
| 3     | Super   |

#### Gem Types

| Gem Type | Normal ItemID | Refined ItemID | Super ItemID | Effect                                                      |
|:---------|:--------------|:---------------|:-------------|:------------------------------------------------------------|
| Phoenix  | 700001        | 700002         | 700003       | +5% / +10% / +15% magic attack                              |
| Dragon   | 700011        | 700012         | 700013       | +5% / +10% / +15% physical attack                           |
| Fury     | 700021        | 700022         | 700023       | +5% / +10% / +15% hitting accuracy                          |
| Rainbow  | 700031        | 700032         | 700033       | +10% / +15% / +25% killing experience                       |
| Kylin    | 700041        | 700042         | 700043       | +50% / +100% / +200% durability                             |
| Violet   | 700051        | 700052         | 700053       | +30% / +50% / +100% weapon experience                       |
| Moon     | 700061        | 700062         | 700063       | +15% / +30% / +50% magic experience                         |
| Tortoise | 700071        | 700072         | 700073       | -2% / -4% / -6% damage taken                                |
| Thunder  | 700101        | 700102         | 700103       | Heaven Fan only: +100 / +300 / +500 Attack & Magic Attack   |
| Glory    | 700121        | 700122         | 700123       | Star Tower only: +100 / +300 / +500 Defense & Magic Defense |

The gem type and quality can be determined by `floor(item_id % 10000 / 10)`. For example, `700011` = type `1` (Dragon), quality `1` (Normal).

### Socket Encoding

The socket byte value is stored in [MsgItemInfo](../network/messages/msgiteminfo.md) (Socket 1 / Socket 2 fields) and is derived from the gem's item ID:

```
socket_byte = item_id % 1000
```

For example, Super Dragon Gem (`700013`): `700013 % 1000 = 13`.

#### Socket Values

```protobuf
enum SocketedGem {
  NO_SOCKET        = 0;

  PHOENIX_NORMAL   = 1;
  PHOENIX_REFINED  = 2;
  PHOENIX_SUPER    = 3;

  DRAGON_NORMAL    = 11;
  DRAGON_REFINED   = 12;
  DRAGON_SUPER     = 13;

  FURY_NORMAL      = 21;
  FURY_REFINED     = 22;
  FURY_SUPER       = 23;

  RAINBOW_NORMAL   = 31;
  RAINBOW_REFINED  = 32;
  RAINBOW_SUPER    = 33;

  KYLIN_NORMAL     = 41;
  KYLIN_REFINED    = 42;
  KYLIN_SUPER      = 43;

  VIOLET_NORMAL    = 51;
  VIOLET_REFINED   = 52;
  VIOLET_SUPER     = 53;

  MOON_NORMAL      = 61;
  MOON_REFINED     = 62;
  MOON_SUPER       = 63;

  TORTOISE_NORMAL  = 71;
  TORTOISE_REFINED = 72;
  TORTOISE_SUPER   = 73;

  THUNDER_NORMAL   = 101;
  THUNDER_REFINED  = 102;
  THUNDER_SUPER    = 103;

  GLORY_NORMAL     = 121;
  GLORY_REFINED    = 122;
  GLORY_SUPER      = 123;

  EMPTY_SOCKET     = 255;
}
```

`NO_SOCKET = 0` means the equipment has no socket in that slot. `EMPTY_SOCKET = 255` means the socket exists in the equipment but has no gem socketed.

