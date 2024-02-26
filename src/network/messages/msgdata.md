# MsgData

This message is sent by the game server to update the client interface with a series of integer values. The main usage of this message is to sync the client with the date and time of the server, and was introduced with the watercolor client. In later versions of the client, it was used again for displaying mount vigor.

## Table of Contents

* [Patch 5031](#patch-5031)
* [Patch 5165](#patch-5165)

## Patch 5031

#### Message Definition

☑️ Assumed (Observed) - Chimera

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 36 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1033 |
| 4  | UInt32 | [Data Type](#data-type) | How to processes the message | 0 |
| 8  | UInt32[] | Data Values | Array of data values | |

#### Data Type

☑️ Assumed (Observed) - Chimera

| Val | Name | Description | Data |
|:----|:--------|:--------|:--------|
| 0  | DATETIME | Set server datetime | Year, month, weekday, day, hour, minute, second |

## Patch 5165

#### Message Definition

☑️ Assumed (Observed) - Chimera

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 36 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1033 |
| 4  | UInt32 | [Data Type](#data-type-1) | How to processes the message | 0 |
| 8  | UInt32[] | Data Values | Array of data values | |

#### Data Type

☑️ Assumed (Observed) - Chimera

| Val | Name | Description | Data |
|:----|:--------|:--------|:--------|
| 0  | DATETIME | Set server datetime | Year, month, weekday, day, hour, minute, second |
| 2  | VIGOR | Set mount vigor (move points) | Vigor |
