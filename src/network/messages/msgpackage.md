# MsgPackage

This message is sent between the client and game server to handle item storage, such as warehouses, chests in houses, and sashes in later versions of Conquer Online.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5187](#patch-5187)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

The message definition below is used for basic requests on checking in and out items.

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 14 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1102 |
| 4  | UInt32 | [ID](/network/identifiers.md) | Identifier for a hero, NPC, or trunk | 8 |
| 8  | Byte | [Action](#action-type) | How to processes the message | 0 |
| 9  | Byte | [Type](#package-type) | The type of package being processed | 10 |
| 10 | UInt32 | [Item ID](/network/identifiers.md) | Unique identifier of the item | 1 |

The message definition below is used for returning a list of items back to the player.

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1102 |
| 4  | UInt32 | [ID](/network/identifiers.md) | Identifier for a hero, NPC, or trunk | 8 |
| 8  | Byte | [Action](#action-type) | How to processes the message | 0 |
| 9  | Byte | [Type](#package-type) | The type of package being processed | 10 |
| 10 | UInt16 | Amount | Amount of items to send | 1 |
| 12 | [PackageItem](#package-item-definition)[] | Items | Abbreviated item infos | |

#### Package Item Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt32 | [Item ID](/network/identifiers.md) | Unique identifier of the item | 1 |
| 4  | UInt32 | [Item Type](/files/content/itemtype.dat.md) | Identifies the type of item | 730001 |
| 8  | Byte | [Status](msgiteminfo.md#item-status) | Condition bit flags on the item | 0 |
| 9  | Byte | [Socket](/algorithms/rates/item-sockets.md) 1 | The [gem](/constants/gem.md) in the first socket position | 0 |
| 10 | Byte | [Socket](/algorithms/rates/item-sockets.md) 2 | The [gem](/constants/gem.md) in the second socket position | 0 |
| 11 | Byte | Magic 1 | Reserved for rebirth magic effect | 0 |
| 12 | Byte | Magic 2 | Reserved for an unknown purpose | 0 |
| 13 | Byte | Magic 3 | Reserved for magical [plus](/algorithms/rates/item-composition.md) rating | 0 |
| 14 | Byte | Bless | Reduced damage percentage taken by the character | 0 |
| 15 | Byte | Enchant | Added max life for the character | 0 |

#### Action Type

☑️ Assumed (Observed) - CoFuture + Soul

| Val | Name | Description | Recipient | ID | Data |
|:----|:--------|:--------|:--------|:--------|:--------|
| 0 | QUERY_LIST | Query for a list of items | Server | [NPC ID](/network/identifiers.md) | [PackageItem](#package-item-definition)[] |
| 1 | CHECK_IN | Deposit an item | Server | [NPC ID](/network/identifiers.md) | ItemID |
| 2 | CHECK_OUT | Withdraw an item | Server | [NPC ID](/network/identifiers.md) | ItemID |

#### Package Type

☑️ Assumed (Observed) - CoFuture + Soul

```proto
enum PackageType {

    PACKAGE_TYPE_NONE = 0;
    PACKAGE_TYPE_STORAGE = 10;
    PACKAGE_TYPE_TRUNK = 20;
}
```

## Patch 5187

#### Message Definition

❓ Unverified

The message definition below is used for basic requests on checking in and out items.

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 14 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1102 |
| 4  | UInt32 | [ID](/network/identifiers.md) | Identifier for a hero, NPC, or trunk | 8 |
| 8  | Byte | [Action](#action-type-1) | How to processes the message | 0 |
| 9  | Byte | [Type](#package-type-1) | The type of package being processed | 10 |
| 10 | UInt32 | [Item ID](/network/identifiers.md) | Unique identifier of the item | 1 |

The message definition below is used for returning a list of items back to the player.

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 38 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1102 |
| 4  | UInt32 | [ID](/network/identifiers.md) | Identifier for a hero, NPC, or trunk | 8 |
| 8  | Byte | [Action](#action-type-1) | How to processes the message | 0 |
| 9  | Byte | [Type](#package-type-1) | The type of package being processed | 10 |
| 10 | UInt16 | Amount | Amount of items to send | 1 |
| 12 | [PackageItem](#package-item-definition-1)[] | Items | Abbreviated item infos | |

#### Package Item Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt32 | [Item ID](/network/identifiers.md) | Unique identifier of the item | 1 |
| 4  | UInt32 | [Item Type](/files/content/itemtype.dat.md) | Identifies the type of item | 730001 |
| 8  | Byte | [Status](msgiteminfo.md#item-status) | Condition bit flags on the item | 0 |
| 9  | Byte | [Socket](/algorithms/rates/item-sockets.md) 1 | The [gem](/constants/gem.md) in the first socket position | 0 |
| 10 | Byte | [Socket](/algorithms/rates/item-sockets.md) 2 | The [gem](/constants/gem.md) in the second socket position | 0 |
| 11 | Byte | Magic 1 | Reserved for rebirth magic effect | 0 |
| 12 | Byte | Magic 2 | Reserved for an unknown purpose | 0 |
| 13 | Byte | Magic 3 | Reserved for magical [plus](/algorithms/rates/item-composition.md) rating | 0 |
| 14 | Bool | Bound | True if the item is bound to an account | 0 |
| 15 | Byte | Bless | Reduced damage percentage taken by the character | 0 |
| 16 | Byte | Enchant | Added max life for the character | 0 |
| 17 | UInt16 | Data | Additional attributes for the item | 0 |
| 19 | Bool | Suspicious | Marked as suspicious for trading | 0 |
| 20 | Bool | Locked | Locked from being dropped or traded | 0 |
| 21 | Byte | [Color](msgiteminfo.md#item-color) | Color modifier for the item | 3 |
| 22 | UInt32 | Magic 3 Progress | Progress towards magical [plus](/algorithms/rates/item-composition.md) rating | 0 |

#### Action Type

❓ Unverified

| Val | Name | Description | Recipient | ID | Data |
|:----|:--------|:--------|:--------|:--------|:--------|
| 0 | QUERY_LIST | Query for a list of items | Server | [NPC ID](/network/identifiers.md) | [PackageItem](#package-item-definition)[] |
| 1 | CHECK_IN | Deposit an item | Server | [NPC ID](/network/identifiers.md) | ItemID |
| 2 | CHECK_OUT | Withdraw an item | Server | [NPC ID](/network/identifiers.md) | ItemID |

#### Package Type

❓ Unverified

```proto
enum PackageType {

    PACKAGE_TYPE_NONE = 0;
    PACKAGE_TYPE_STORAGE = 10;
    PACKAGE_TYPE_TRUNK = 20;
    PACKAGE_TYPE_SASH = 30;
}
```
