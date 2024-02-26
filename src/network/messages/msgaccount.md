# MsgAccount

This client message is sent to the account server to request authentication. There have been multiple message types over the years for handling authentication requests from the client. MsgAccount is the first, but was later replaced by [MsgAccountSRP6](msgaccountsrp6.md) and [MsgAccountSRP6Ex](msgaccountsrp6ex.md) in versions 5532+.

In this message, the player's password is encrypted using [RC5](/security/rc5.md).

> ⚠️ __WARNING__
>
> The password in this message is encrypted using a static key in earlier versions of the client. Although later versions start to use a generated key, that key is exchanged using [MsgEncryptCode](msgencryptcode.md) and does not protect against proxies employing a man-in-the-middle attack. This was patched in version 5532 with the use of [SRP6](/security/srp6.md), which also added additional complexity for clientless bot creation.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5165](#patch-5165)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 52 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1051 |
| 4  | Char[16] | Account | Fixed string of the username | Player |
| 20 | Char[16] | Password | Encrypted buffer containing the password | RC5(Password) |
| 36 | Char[16] | Server | Fixed string of the game server | Meteor |

## Patch 5165

#### Message Definition

✅ Verified (Client)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 276 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1086 |
| 4  | Char[128] | Account | Fixed string of the username | Player |
| 132 | Char[128] | Password | Encrypted buffer containing the password | RC5(Password) |
| 260 | Char[16] | Server | Fixed string of the game server | Meteor |
