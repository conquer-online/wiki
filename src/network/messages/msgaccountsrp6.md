# MsgAccountSRP6

This client message is sent to the account server to request authentication using [SRP6](../../security/srp6.md) as an augmented password-authenticated key exchange, replacing the previous [MsgAccount](msgaccount.md) message that used an RC5 encrypted password in patch 5532. The messages are similar, but the password field has been removed.

Before handling this message, an account needs to be created using a password verifier and salt rather than a password. The account server is expected look up the account's password verifier in the database to send [MsgLoginChallengeS](msgloginchallenges.md) in response to this message.

## Table of Contents

* [Patch 5635](#patch-5635)

## Patch 5635

#### Message Definition

☑️ Assumed (Observed)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 240 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1124 |
| 8  | Char[128] | Account | Fixed string of the username | Player |
| 136 | Char[16] | Server | Fixed string of the game server | Meteor |
