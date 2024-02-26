# MsgPCNum

This client message is sent to the account server after receiving [MsgConnectEx](msgconnectex.md) and contains the client's mac address. The mac address field in this message is trailed by a null terminator at offset 48 (explicitly set by the client).

## Table of Contents

* [Patch 5615](#patch-5615)

## Patch 5615

#### Message Definition

✅ Verified (Client)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 52 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1100 |
| 4  | UInt32 | [Account ID](/network/identifiers.md) | Account id from the account server | 1 |
| 8  | Char[40] | Mac address | Mac address for the client interface | 0A0B0C0D0E0F |
