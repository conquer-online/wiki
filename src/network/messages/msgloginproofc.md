# MsgLoginProofC

The client sends this message back to the account server in response to [MsgLoginChallengeS](msgloginchallenges.md) for completing the [SRP6](../../security/srp6.md) challenge. The response contains the client's proof of K (the client key C). The account server is expected to complete its own proof of K (server key M), which it then compares against C. It then sends [MsgConnectEx](msgconnectex.md) to either accept or reject the client.

> ⚠️ __WARNING__
>
> The server should always verify that the client's proof of K and public ephemeral value are non-zero.

## Table of Contents

* [Patch 5635](#patch-5635)

## Patch 5635

#### Message Definition

☑️ Assumed (Observed)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0   | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 262 |
| 2   | UInt16 | [MsgType](index.md#message-header) | Type of message | 1214 |
| 4   | Byte | A Length | Client's public ephemeral length | |
| 5   | Byte[] | A | Client's public ephemeral value | |
| 133 | Byte | C Length | Client's proof of K length | |
| 134 | Byte[] | C | Client's proof of K | |
