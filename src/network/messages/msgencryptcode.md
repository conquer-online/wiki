# MsgEncryptCode

This message is sent from the account server to the client when it first connects to initialize the [RC5](/security/rc5.md) cipher used for encrypting the player's password. The client then responds to this message with [MsgAccount](msgaccount.md). In later versions of the client, this message is sent but never utilized. This is to keep the account server compatible with older versions of the client / different games.

## Table of Contents

* [Patch 5187](#patch-5187)

## Patch 5187

#### Message Definition

✅ Verified (Client)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0 | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 8 |
| 2 | UInt16 | [MsgType](index.md#message-header) | Type of message | 1059 |
| 4 | UInt32 | Seed | Generated seed for RC5 | 10000 |