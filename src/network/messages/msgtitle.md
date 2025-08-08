# MsgTitle

Player titles are earned through in-game events, and can be collected, selected, and removed by the player. This message allows players to view and manager their titles. Titles are associated with an ID, defined in the client's Title.ini file.

## Table of Contents

* [Patch 5635](#patch-5635)

## Patch 5635

#### Message Definition

✅ Verified (Client)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 12 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1130 |
| 4  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | Byte | TitleID | Title ID as it appears in Title.ini | 11 |
| 9  | Byte | [Action](#title-action) | How to process the message | 4 |
| 10 | Byte | Amount | Number of titles to list | 1 |
| 11 | Byte[] | Titles | An array of titles | 11 |

#### Title Action

✅ Verified (Client)

| Val | Name | Description | Recipient |
|:------|:--------|:--------|:--------|
| 1 | ADD_TITLE | Adds a title | Client |
| 2 | LOSE_TITLE | Removes a title | Client |
| 3 | SET_TITLE | Sets a title for the player | Both |
| 4 | LIST_TITLES | Gets titles for the player | Both |
