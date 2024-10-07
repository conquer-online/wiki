# MsgRegister

This message is sent from the game client containing initial character creation details from the character creation screen. To get this message, you must first send [MsgTalk](msgtalk.md) with the text "NEW_ROLE" on the login attribute. The expected response to this message from the server is [MsgTalk](msgtalk.md) with the text "ANSWER_OK" on the register attribute. Invalid registration attempts can be answered with the error on the register attribute rather than with "ANSWER_OK".

The identity shown in this message may not be the account identifier if you use an access token in place of the identifier in [MsgConnectEx](msgconnectex.md).

> ⚠️ __WARNING__
>
> Character creation requests can be easily spoofed with invalid professions and models, so be sure to validate inputs. Character names may also contain invalid characters or phrases, such as "[GM]" or "[PM]".

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5017](#patch-5017)
* [Patch 5065](#patch-5065)
* [Patch 5165](#patch-5165)

## Patch 4267

#### Message Definition

❓ Unverified - Imported from the legacy wiki

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 60 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1001 |
| 4  | Char[16] | [Username](../../strings/accountusername.md) | Account username from login | admin |
| 20 | Char[16] | [Hero Name](../../strings/heroname.md) | Requested name to be checked | Player |
| 36 | Char[16] | [Password](../../strings/accountpassword.md) | Account password (missing RC5 wrapper) | test |
| 52 | UInt16 | [Hero Look](../../constants/herolook.md) | Selected character model | 1003 |
| 54 | UInt16 | [Hero Profession](../../constants/heroprofession.md) | Selected character profession | 10 |
| 56 | UInt32 | [Account ID](../identifiers.md) | Account id from the account server | 1 |

## Patch 5017

#### Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 60 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1001 |
| 4  | Char[16] | [Username](../../strings/accountusername.md) | Account username from login | admin |
| 20 | Char[16] | [Hero Name](../../strings/heroname.md) | Requested name to be checked | Player |
| 36 | Char[16] | Masked Password | Hidden password | **** |
| 52 | UInt16 | [Hero Look](../../constants/herolook.md) | Selected character model | 1003 |
| 54 | UInt16 | [Hero Profession](../../constants/heroprofession.md) | Selected character profession | 10 |
| 56 | UInt32 | [Account ID](../identifiers.md) | Account id from the account server | 1 |

## Patch 5065

#### Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 60 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1001 |
| 4  | Char[16] | [Username](../../strings/accountusername.md) | Account username from login | admin |
| 20 | Char[16] | [Hero Name](../../strings/heroname.md) | Requested name to be checked | Player |
| 52 | UInt16 | [Hero Look](../../constants/herolook.md) | Selected character model | 1003 |
| 54 | UInt16 | [Hero Profession](../../constants/heroprofession.md) | Selected character profession | 10 |
| 56 | UInt32 | [Account ID](../identifiers.md) | Account id from the account server | 1 |

## Patch 5165

#### Message Definition

❓ Unverified - Imported from the legacy wiki

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 104 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1001 |
| 4  | Char[16] | [Username](../../strings/accountusername.md) | Account username from login | admin |
| 20 | Char[16] | [Hero Name](../../strings/heroname.md) | Requested name to be checked | Player |
| 52 | UInt16 | [Hero Look](../../constants/herolook.md) | Selected character model | 1003 |
| 54 | UInt16 | [Hero Profession](../../constants/heroprofession.md) | Selected character profession | 10 |
| 56 | UInt32 | [Account ID](../identifiers.md) | Account id from the account server | 1 |
| 60 | UInt16[6] | MacAddress | Network device identifier | 00,10,5A,44,12,B5 |