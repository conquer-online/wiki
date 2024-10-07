# MsgGemEmbed

This message is sent by the client to request embedding or removing a gem in an item.

> ⚠️ __WARNING__
>
> Ensure that the identifier of the gem is a valid gem. It's possible that a modified game client can send a message containing a gem ID that's the same as the item identifier. In that case, a poorly validated server could add a gem based on the item type (could be deterministic).

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 20 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1027 |
| 4  | UInt32 | User | [Hero ID](../identifiers.md) of the player | 1000001 |
| 8  | UInt32 | Item | Identifier for the item | 1 |
| 12 | UInt32 | [Gem](../../constants/gem.md) | Identifier for the gem | 2 |
| 16 | UInt16 | Pos | Gem [socket](../../algorithms/rates/item-sockets.md) to embed into or remove from | 1 |
| 18 | UInt16 | [Action](#action-type) | Embed or remove the gem | 0 |

#### Action Type

☑️ Assumed (Soul)

```proto
enum GemEmbedActionType {

    GEM_EMBED_ACTION_EMBED = 0;
    GEM_EMBED_ACTION_REMOVE = 1;
}
```
