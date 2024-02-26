# MsgFriend

This message is sent by clients to manage friend requests and their friend and enemy lists. It's also sent by the game server to populate those lists on sign-on, update online statuses, after accepting a friend request, and after a player kill.

The level parameter that once appeared at offset 10 was removed during the alpha for Conquer Online in favor of the [MsgFriendInfo](msgfriendinfo.md) message.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5017](#patch-5017)
* [Patch 5615](#patch-5615)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - Soul + CoFuture

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1019 |
| 4  | UInt32 | [Hero ID](/network/identifiers.md) | Unique identifier for the friend | 1000000 |
| 8 | Byte | [Action](#action-type) | How to processes the message | 11 |
| 9 | Byte | IsOnline | True if the friend is online | 1 |
| 12 | Char[16] | Name | Character name as a fixed string | Player |

#### Action Type

☑️ Assumed (Soul)

```proto
enum FriendActionTypes {

    FRIEND_APPLY = 10;
    FRIEND_ACCEPT = 11;
    FRIEND_ONLINE = 12;
    FRIEND_OFFLINE = 13;
    FRIEND_BREAK = 14;
    FRIEND_GETINFO = 15;

    ENEMY_ONLINE = 16;
    ENEMY_OFFLINE = 17;
    ENEMY_DELETE = 18;
    ENEMY_ADD = 19;
}
```

## Patch 5017

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 36 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1019 |
| 4  | UInt32 | [Hero ID](/network/identifiers.md) | Unique identifier for the friend | 1000000 |
| 8 | Byte | [Action](#action-type-1) | How to processes the message | 11 |
| 9 | Byte | Is Online | True if the friend is online | 1 |
| 12 | UInt32 | Nobility Rank | Nobility ranking | 3 |
| 16 | UInt32 | Flower Rank | Flower ranking | 0 |
| 20 | Char[16] | Name | Character name as a fixed string | Player |

#### Action Type

☑️ Assumed (Soul)

```proto
enum FriendActionTypes {

    FRIEND_APPLY = 10;
    FRIEND_ACCEPT = 11;
    FRIEND_ONLINE = 12;
    FRIEND_OFFLINE = 13;
    FRIEND_BREAK = 14;
    FRIEND_GETINFO = 15;

    ENEMY_ONLINE = 16;
    ENEMY_OFFLINE = 17;
    ENEMY_DELETE = 18;
    ENEMY_ADD = 19;
}
```

## Patch 5615

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 68 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1019 |
| 4  | UInt32 | [Hero ID](/network/identifiers.md) | Unique identifier for the friend | 1000000 |
| 8 | Byte | [Action](#action-type-1) | How to processes the message | 11 |
| 9 | Byte | Is Online | True if the friend is online | 1 |
| 12 | UInt32 | Nobility Rank | Nobility ranking | 3 |
| 16 | UInt32 | Flower Rank | Flower ranking | 0 |
| 20 | Char[16] | Name | Character name as a fixed string | Player |
| 36 | Char[32] | Facebook ID | Identifier for Facebook Profile | |

#### Action Type

☑️ Assumed (Soul)

```proto
enum FriendActionTypes {

    FRIEND_APPLY = 10;
    FRIEND_ACCEPT = 11;
    FRIEND_ONLINE = 12;
    FRIEND_OFFLINE = 13;
    FRIEND_BREAK = 14;
    FRIEND_GETINFO = 15;

    ENEMY_ONLINE = 16;
    ENEMY_OFFLINE = 17;
    ENEMY_DELETE = 18;
    ENEMY_ADD = 19;
}
```