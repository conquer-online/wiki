# MsgGameServerShutDown

This message is sent by the game server to the client to request a polite disconnect. Sending this message to the client causes an error state and spawns a message.

## Table of Contents

* [Patch 5635](#patch-5635)

## Patch 5635

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 12 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1350 |
| 4  | UInt32 | [Action](#shutdown-action) | How the message will be processed | 0 |
| 8  | UInt32 | Message ID | The message to display | 10 |

#### Shutdown Action

❓ Unverified

```proto
enum ShutdownAction {

    DEFAULT = 0;
}
```