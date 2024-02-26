# MsgConnect

This client message is first sent to the account server after receiving [MsgConnectEx](msgconnectex.md), and then sent to the game server after the client disconnects from the account server and connects to the game server specified in [MsgConnectEx](msgconnectex.md). The game server is expected to respond to this connection attempt with [MsgTalk](msgtalk.md) (see this message type for details on that interaction).

The account ID in the account server MsgConnect message is copied from [MsgConnectEx](msgconnectex.md), and the account ID and data fields in the game server MsgConnect message are also copied from [MsgConnectEx](msgconnectex.md).

> ⚠️ __WARNING__
>
> A **serious exploit** is possible using this message on some servers. If a deterministic key is used, such as the account ID, an encrypted account ID, or incrementor, then it may be possible for any bad actor to log into any character in the game (bypassing the account server).
>
> The following are some example fixes employed in various server projects for replacing the two 32-bit fields:
>
> * Short-lived access token sent from the account server to the game server over RPC, paired with the connector's IP address and account ID.
> * Short-lived connection request record stored in a shared database containing the connector's IP address and account ID.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 4343](#patch-4343)
* [Patch 5065](#patch-5065)

## Patch 4267

#### Account Server Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1052 |
| 4  | UInt32 | [Account ID](/network/identifiers.md) | Account id from the account server | 1 |
| 8  | UInt32 | Data | Contents of the [Res.dat](/files/content/res.dat.md) file | 10 |
| 12 | Char[16] | Info | Name of the file | Res.dat |

#### Game Server Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1052 |
| 4  | UInt32 | [Account ID](/network/identifiers.md) | Account id from the account server | 1 |
| 8  | UInt32 | Data | [Encryption key](/security/tq.md) generator parameter | 6351601 |
| 12 | Char[16] | Info | Build version and language | 117 English |

## Patch 4343

#### Account Server Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1052 |
| 4  | UInt32 | [Account ID](/network/identifiers.md) | Account id from the account server | 1 |
| 8  | UInt32 | Data | Contents of the [Res.dat](/files/content/res.dat.md) file | 10 |
| 12 | Char[16] | Info | Name of the file | Res.dat |

#### Game Server Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1052 |
| 4  | UInt32 | [Account ID](/network/identifiers.md) | Account id from the account server | 1 |
| 8  | UInt32 | Data | [Encryption key](/security/tq.md) generator parameter | 6351601 |
| 12 | UInt16 | Build | Build version of the client | 123 |
| 14 | Char[10] | Language | [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) language code | En |
| 24 | UInt32 | Info | Contents of the [Res.dat](/files/content/res.dat.md) file | 10 |

## Patch 5065

#### Account Server Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1052 |
| 4  | UInt32 | [Account ID](/network/identifiers.md) | Account id from the account server | 1 |
| 8  | UInt32 | Data | Contents of the [Res.dat](/files/content/res.dat.md) file | 10 |
| 12 | Char[16] | Info | Name of the file | Res.dat |

#### Game Server Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1052 |
| 4  | UInt32 | [Account ID](/network/identifiers.md) | Account id from the account server | 1 |
| 8  | UInt32 | Data | [Encryption key](/security/tq.md) generator parameter | 6351601 |
| 12 | UInt16 | Build | Build version of the client | 123 |
| 14 | Char[2] | Language | [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) language code | En |
| 16 | Char[8] | Mac Address | Mac address of connecting interface | 0A0B0C0D0E0F |
| 24 | UInt32 | Info | Contents of the [Res.dat](/files/content/res.dat.md) file | 10 |
