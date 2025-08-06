# MsgAccountSRP6Ex

This client message is sent to the account server to request authentication using [SRP6](../../security/srp6.md) as an augmented password-authenticated key exchange, replacing the previous [MsgAccountSRP6](msgaccountsrp6.md) message. It combines [MsgAccountSRP6](msgaccountsrp6.md), [MsgConnect](msgconnect.md), [MsgEncryptCode](msgencryptcode.md), and [MsgPCNum](msgpcnum.md) into a single message, and implements a random buffer used as a key derivation function (KDF) in SRP6.

Before handling this message, an account needs to be created using a password verifier and salt rather than a password. The account server is expected look up the account's password verifier in the database to send [MsgLoginChallengeS](msgloginchallenges.md) in response to this message.

## Table of Contents

* [Patch 5635](#patch-5635)

## Patch 5635

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 312 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1636 |
| 8  | Char[128] | Account | Fixed string of the username | Player |
| 136 | Char[16] | Server | Fixed string of the game server | Meteor |
| 152 | Char[16] | Mac Address | Mac address of connecting interface | 0A0B0C0D0E0F |
| 193 | Char[4] | Data | Contents of the [Res.dat](../../files/content/res.dat.md) file | 0010 |
| 244 | Byte[64] | Random | Random buffer used as a KDF in SRP6 | |
| 308 | UInt32 | EncryptCode | Exchange seed for SRP6 | 10000 |
