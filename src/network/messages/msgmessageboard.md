# MsgMessageBoard

Message boards are categorized into channels, referenced in [MsgTalk](msgtalk.md) as [Text Attributes](msgtalk.md#text-attribute). The game server and client pass this message to organize text messages from MsgTalk into listable postings.

The [NetStringPacker](../stringpacker.md) returned when listing posts (10 maximum) is flattened groupings of three strings each:

* Name: The name of the hero who authored the message.
* Message: Text shortened to 36 characters.
* Date: In the format yyyyMMddHHmmss.

## Table of Contents

* [Patch 5017](#patch-5017)

## Patch 5017

#### Message Definition

☑️ Assumed (Observed) - Soul + COPSv6

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 9 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1111 |
| 4  | UInt16 | Index | Message index for continuation | 0 |
| 6  | UInt16 | Channel | [Text Attributes](msgtalk.md#text-attribute) | 2201 |
| 8  | Byte | [Action](#message-board-action) | Message action type | 2 |
| 9 | [NetStringPacker](../stringpacker.md) | Strings | | |

#### Message Board Action

☑️ Assumed (Observed) - Soul + COPSv6

| Val | Name | Description | Recipient | Strings |
|:------|:--------|:--------|:--------|:--------|
| 1 | DEL | Deletes a message on the board | Server | 1 4 Hero |
| 2 | GET_LIST | Fetches list of messages by index | Server | |
| 3 | LIST | List of messages for a requested index | Client | (See format) |
| 4 | GET_WORDS | Request [MsgTalk](msgtalk.md) message for a post | Server | |
