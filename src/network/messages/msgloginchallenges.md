# MsgLoginChallengeS

The account server sends this message to client to start the [SRP6](../../security/srp6.md) challenge. The challenge consists of the calculated public ephemeral value (B = kv + g^b mod |N|) and the player's salt (S). The client expects this message in response to [MsgAccountSRP6](msgaccountsrp6.md) / [MsgAccountSRP6Ex](msgaccountsrp6ex.md), and responds with [MsgLoginProofC](msgloginproofc.md).

## Table of Contents

* [Patch 5635](#patch-5635)

## Patch 5635

#### Message Definition

☑️ Assumed (Observed)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0   | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 653 |
| 2   | UInt16 | [MsgType](index.md#message-header) | Type of message | 1213 |
| 4   | Byte | B Length | Server's public ephemeral length | |
| 5   | Byte[] | B | Server's public ephemeral value | |
| 391 | Byte | S Length | Salt length | |
| 392 | Byte[] | S | The player's salt | |
