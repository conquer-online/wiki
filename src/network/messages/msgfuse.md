# MsgFuse

This message is sent by the client to request fusing materials to an item. Though the system isn't officially used by non-Chinese Conquer Online or translated in the interface, it is implemented in the client and can be utilized by private servers. Fuse rates come from [fuse.ini](../../files/content/fuse.ini.md), and successfully fused items result in a +1 stone (according to unverified sources).

Some private servers have repurposed this interface to quickly attempt a socket on an included item using meteor scrolls and other loose meteors.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 22 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1028 |
| 4  | UInt32 | User | [Hero ID](../identifiers.md) of the player | 1000001 |
| 8  | UInt16 | Action | The type of fuse being performed | 0 |
| 10 | UInt32 | Count | The number of items included | 2 |
| 14 | UInt32[] | Items | Array of [item IDs](../identifiers.md) | |