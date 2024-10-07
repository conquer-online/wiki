# MsgItemInfo

This message is sent to the game client from the game server to initialize an item, which can appear in the player's inventory, as equipment, or in another position within the client's UI. Some exceptions to this include detained items ([MsgDetainItemInfo](msgdetainiteminfo.md)) and shop / present items ([MsgItemInfoEx](msgiteminfoex.md)).

In later versions of the client (around patch 5200), [MsgPlayerAttribInfo](msgplayerattribinfo.md) was added to update the role view separately from equipment being placed in a player's equipment slot. The purpose of splitting off attributes from  items was to enable temporary boons and weaknesses.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 4330](#patch-4330)
* [Patch 5017](#patch-5017)
* [Patch 5095](#patch-5095)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 24 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1008 |
| 4  | UInt32 | [Item ID](../identifiers.md) | Unique identifier for the item (unless someone else's item) | 1 |
| 8  | UInt32 | [Item Type](../../files/content/itemtype.dat.md) | Identifies the type of item | 730001 |
| 12 | UInt16 | Amount | Current [durability](../../algorithms/calculations/item-durability.md) or amount of the item | 10000 |
| 14 | UInt16 | Max Amount | Total [durability](../../algorithms/calculations/item-durability.md) or amount the item can have | 10000 |
| 16 | Byte | [Action](#action-type) | How item info should be processed | 1 |
| 17 | Byte | [Status](#item-status) | Condition bit flags on the item | 0 |
| 18 | Byte | [Position](#item-position) | Position where the item appears | 0 |
| 19 | Byte | [Socket](../../algorithms/rates/item-sockets.md) 1 | The [gem](../../constants/gem.md) in the first socket position | 0 |
| 20 | Byte | [Socket](../../algorithms/rates/item-sockets.md) 2 | The [gem](../../constants/gem.md) in the second socket position | 0 |
| 21 | Byte | Magic 1 | Reserved for rebirth magic effect | 0 |
| 22 | Byte | Magic 2 | Reserved for an unknown purpose | 0 |
| 23 | Byte | Magic 3 | Reserved for magical [plus](../../algorithms/rates/item-composition.md) rating | 0 |

#### Action Type

☑️ Assumed (Soul)

```proto
enum ItemInfoActionType {

    ITEMINFO_NONE = 0;
    ITEMINFO_ADDITEM = 1;
    ITEMINFO_TRADE = 2;
    ITEMINFO_UPDATE = 3;
    ITEMINFO_OTHERPLAYER_EQUIPMENT = 4;
    ITEMINFO_AUCTION = 5;
}
```

#### Item Status

☑️ Assumed (Soul)

```proto
enum ItemStatus {

    ITEM_STATUS_NONE = 0;
    ITEM_STATUS_UNIDENTIFIED = 0x01;
    ITEM_STATUS_CANNOT_REPAIR = 0x02;
    ITEM_STATUS_FIXED_DURABILITY = 0x04;
    ITEM_STATUS_MAGIC_ADD = 0x08;
}
```

#### Item Position

☑️ Assumed (Soul)

```proto
enum ItemPosition {

    ITEMPOSITION_INVENTORY = 0;
    ITEMPOSITION_HELMET = 1;
    ITEMPOSITION_NECKLACE = 2;
    ITEMPOSITION_ARMOR = 3;
    ITEMPOSITION_WEAPON_RIGHT = 4;
    ITEMPOSITION_WEAPON_LEFT = 5;
    ITEMPOSITION_RING = 6;
    ITEMPOSITION_TREASURE = 7;
    ITEMPOSITION_BOOTS = 8;

    ITEMPOSITION_STORAGE = 201;
    ITEMPOSITION_TRUNK = 202;
    ITEMPOSITION_TREASURE_BAG = 203;
    ITEMPOSITION_AUCTION_STORAGE = 207;

    ITEMPOSITION_GROUND = 254;
    ITEMPOSITION_NONE = 255;
}
```

## Patch 4330

#### Message Definition

☑️ Assumed (Observed) - COPSv6 Enhanced

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 30 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1008 |
| 4  | UInt32 | [Item ID](../identifiers.md) | Unique identifier for the item (unless someone else's item) | 1 |
| 8  | UInt32 | [Item Type](../../files/content/itemtype.dat.md) | Identifies the type of item | 730001 |
| 12 | UInt16 | Amount | Current [durability](../../algorithms/calculations/item-durability.md) or amount of the item | 10000 |
| 14 | UInt16 | Max Amount | Total [durability](../../algorithms/calculations/item-durability.md) or amount the item can have | 10000 |
| 16 | Byte | [Action](#action-type-1) | How item info should be processed | 1 |
| 17 | Byte | [Status](#item-status-1) | Condition bit flags on the item | 0 |
| 18 | Byte | [Position](#item-position-1) | Position where the item appears | 0 |
| 19 | Byte | [Socket](../../algorithms/rates/item-sockets.md) 1 | The [gem](../../constants/gem.md) in the first socket position | 0 |
| 20 | Byte | [Socket](../../algorithms/rates/item-sockets.md) 2 | The [gem](../../constants/gem.md) in the second socket position | 0 |
| 21 | Byte | Magic 1 | Reserved for rebirth magic effect | 0 |
| 22 | Byte | Magic 2 | Reserved for an unknown purpose | 0 |
| 23 | Byte | Magic 3 | Reserved for magical [plus](../../algorithms/rates/item-composition.md) rating | 0 |
| 24 | Byte | Bless | Reduced damage percentage taken by the character | 0 |
| 25 | Byte | Enchant | Added max life for the character | 0 |
| 26 | UInt32 | Data | Additional attributes for the item | 0 |

#### Action Type

☑️ Assumed (Soul)

```proto
enum ItemInfoActionType {

    ITEMINFO_NONE = 0;
    ITEMINFO_ADDITEM = 1;
    ITEMINFO_TRADE = 2;
    ITEMINFO_UPDATE = 3;
    ITEMINFO_OTHERPLAYER_EQUIPMENT = 4;
    ITEMINFO_AUCTION = 5;
}
```

#### Item Status

☑️ Assumed (Soul)

```proto
enum ItemStatus {

    ITEM_STATUS_NONE = 0;
    ITEM_STATUS_UNIDENTIFIED = 0x01;
    ITEM_STATUS_CANNOT_REPAIR = 0x02;
    ITEM_STATUS_FIXED_DURABILITY = 0x04;
    ITEM_STATUS_MAGIC_ADD = 0x08;
}
```

#### Item Position

☑️ Assumed (Soul)

```proto
enum ItemPosition {

    ITEMPOSITION_INVENTORY = 0;
    ITEMPOSITION_HELMET = 1;
    ITEMPOSITION_NECKLACE = 2;
    ITEMPOSITION_ARMOR = 3;
    ITEMPOSITION_WEAPON_RIGHT = 4;
    ITEMPOSITION_WEAPON_LEFT = 5;
    ITEMPOSITION_RING = 6;
    ITEMPOSITION_TREASURE = 7;
    ITEMPOSITION_BOOTS = 8;

    ITEMPOSITION_STORAGE = 201;
    ITEMPOSITION_TRUNK = 202;
    ITEMPOSITION_TREASURE_BAG = 203;
    ITEMPOSITION_AUCTION_STORAGE = 207;

    ITEMPOSITION_GROUND = 254;
    ITEMPOSITION_NONE = 255;
}
```

## Patch 5017

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 36 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1008 |
| 4  | UInt32 | [Item ID](../identifiers.md) | Unique identifier for the item (unless someone else's item) | 1 |
| 8  | UInt32 | [Item Type](../../files/content/itemtype.dat.md) | Identifies the type of item | 730001 |
| 12 | UInt16 | Amount | Current [durability](../../algorithms/calculations/item-durability.md) or amount of the item | 10000 |
| 14 | UInt16 | Max Amount | Total [durability](../../algorithms/calculations/item-durability.md) or amount the item can have | 10000 |
| 16 | Byte | [Action](#action-type-2) | How item info should be processed | 1 |
| 17 | Byte | [Status](#item-status-2) | Condition bit flags on the item | 0 |
| 18 | Byte | [Position](#item-position-2) | Position where the item appears | 0 |
| 20 | UInt32 | [Socket](../../algorithms/rates/item-sockets.md) Progress | Progress on creating a socket | 0 |
| 24 | Byte | [Socket](../../algorithms/rates/item-sockets.md) 1 | The [gem](../../constants/gem.md) in the first socket position | 0 |
| 25 | Byte | [Socket](../../algorithms/rates/item-sockets.md) 2 | The [gem](../../constants/gem.md) in the second socket position | 0 |
| 26 | Byte | Magic 1 | Reserved for rebirth magic effect | 0 |
| 27 | Byte | Magic 2 | Reserved for an unknown purpose | 0 |
| 28 | Byte | Magic 3 | Reserved for magical [plus](../../algorithms/rates/item-composition.md) rating | 0 |
| 29 | Byte | Bless | Reduced damage percentage taken by the character | 0 |
| 30 | Byte | Enchant | Added max life for the character | 0 |
| 32 | UInt32 | Data | Additional attributes for the item | 0 |

#### Action Type

☑️ Assumed (Soul)

```proto
enum ItemInfoActionType {

    ITEMINFO_NONE = 0;
    ITEMINFO_ADDITEM = 1;
    ITEMINFO_TRADE = 2;
    ITEMINFO_UPDATE = 3;
    ITEMINFO_OTHERPLAYER_EQUIPMENT = 4;
    ITEMINFO_AUCTION = 5;
}
```

#### Item Status

☑️ Assumed (Soul)

```proto
enum ItemStatus {

    ITEM_STATUS_NONE = 0;
    ITEM_STATUS_UNIDENTIFIED = 0x01;
    ITEM_STATUS_CANNOT_REPAIR = 0x02;
    ITEM_STATUS_FIXED_DURABILITY = 0x04;
    ITEM_STATUS_MAGIC_ADD = 0x08;
}
```

#### Item Position

☑️ Assumed (Soul)

```proto
enum ItemPosition {

    ITEMPOSITION_INVENTORY = 0;
    ITEMPOSITION_HELMET = 1;
    ITEMPOSITION_NECKLACE = 2;
    ITEMPOSITION_ARMOR = 3;
    ITEMPOSITION_WEAPON_RIGHT = 4;
    ITEMPOSITION_WEAPON_LEFT = 5;
    ITEMPOSITION_RING = 6;
    ITEMPOSITION_TREASURE = 7;
    ITEMPOSITION_BOOTS = 8;

    ITEMPOSITION_STORAGE = 201;
    ITEMPOSITION_TRUNK = 202;
    ITEMPOSITION_TREASURE_BAG = 203;
    ITEMPOSITION_AUCTION_STORAGE = 207;

    ITEMPOSITION_GROUND = 254;
    ITEMPOSITION_NONE = 255;
}
```

## Patch 5095

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 48 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1008 |
| 4  | UInt32 | [Item ID](../identifiers.md) | Unique identifier for the item (unless someone else's item) | 1 |
| 8  | UInt32 | [Item Type](../../files/content/itemtype.dat.md) | Identifies the type of item | 730001 |
| 12 | UInt16 | Amount | Current [durability](../../algorithms/calculations/item-durability.md) or amount of the item | 10000 |
| 14 | UInt16 | Max Amount | Total [durability](../../algorithms/calculations/item-durability.md) or amount the item can have | 10000 |
| 16 | Byte | [Action](#action-type-2) | How item info should be processed | 1 |
| 17 | Byte | [Status](#item-status-2) | Condition bit flags on the item | 0 |
| 18 | Byte | [Position](#item-position-2) | Position where the item appears | 0 |
| 19 | UInt32 | [Socket](../../algorithms/rates/item-sockets.md) Progress | Progress on creating a socket | 0 |
| 23 | Byte | [Socket](../../algorithms/rates/item-sockets.md) 1 | The [gem](../../constants/gem.md) in the first socket position | 0 |
| 24 | Byte | [Socket](../../algorithms/rates/item-sockets.md) 2 | The [gem](../../constants/gem.md) in the second socket position | 0 |
| 25 | Byte | Magic 1 | Reserved for rebirth magic effect | 0 |
| 26 | Byte | Magic 2 | Reserved for an unknown purpose | 0 |
| 27 | Byte | Magic 3 | Reserved for magical [plus](../../algorithms/rates/item-composition.md) rating | 0 |
| 28 | Byte | Bless | Reduced damage percentage taken by the character | 0 |
| 29 | Bool | Bound | True if the item can't be traded | 0 | 
| 30 | Byte | Enchant | Added max life for the character | 0 |
| 32 | UInt32 | Data | Additional attributes for the item | 0 |
| 36 | Bool | Suspicious | Marked as suspicious for trading | 0 |
| 38 | Bool | Locked | Locked from being dropped or traded | 0 |
| 40 | Byte | [Color](#item-color) | Color modifier for the item | 3 |
| 44 | UInt32 | Magic 3 Progress | Progress towards magical [plus](../../algorithms/rates/item-composition.md) rating | 0 |

#### Action Type

☑️ Assumed (Soul)

```proto
enum ItemInfoActionType {

    ITEMINFO_NONE = 0;
    ITEMINFO_ADDITEM = 1;
    ITEMINFO_TRADE = 2;
    ITEMINFO_UPDATE = 3;
    ITEMINFO_OTHERPLAYER_EQUIPMENT = 4;
    ITEMINFO_AUCTION = 5;
}
```

#### Item Status

☑️ Assumed (Soul)

```proto
enum ItemStatus {

    ITEM_STATUS_NONE = 0;
    ITEM_STATUS_UNIDENTIFIED = 0x01;
    ITEM_STATUS_CANNOT_REPAIR = 0x02;
    ITEM_STATUS_FIXED_DURABILITY = 0x04;
    ITEM_STATUS_MAGIC_ADD = 0x08;
}
```

#### Item Position

☑️ Assumed (Soul)

```proto
enum ItemPosition {

    ITEMPOSITION_INVENTORY = 0;
    ITEMPOSITION_HELMET = 1;
    ITEMPOSITION_NECKLACE = 2;
    ITEMPOSITION_ARMOR = 3;
    ITEMPOSITION_WEAPON_RIGHT = 4;
    ITEMPOSITION_WEAPON_LEFT = 5;
    ITEMPOSITION_RING = 6;
    ITEMPOSITION_TREASURE = 7;
    ITEMPOSITION_BOOTS = 8;

    ITEMPOSITION_STORAGE = 201;
    ITEMPOSITION_TRUNK = 202;
    ITEMPOSITION_TREASURE_BAG = 203;
    ITEMPOSITION_AUCTION_STORAGE = 207;

    ITEMPOSITION_GROUND = 254;
    ITEMPOSITION_NONE = 255;
}
```

#### Item Color

☑️ Assumed (Observed) - Chimera

```proto
enum ItemColor {
    
    ITEMCOLOR_NONE = 0;
    ITEMCOLOR_BLACK = 2;
    ITEMCOLOR_ORANGE = 3;
    ITEMCOLOR_TEAL = 4;
    ITEMCOLOR_RED = 5;
    ITEMCOLOR_BLUE = 6;
    ITEMCOLOR_YELLOW = 7;
    ITEMCOLOR_PURPLE = 8;
    ITEMCOLOR_WHITE = 9;
}
```
