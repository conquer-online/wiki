# MsgNpc

This message is sent to the game server to interact with an NPC. This is mostly used to activate an NPC for a shop or dialog, but can also be used to place and delete player furniture. This same feature can be used from PM menus to add and delete any NPC using the client as an editor.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 16 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 2031 |
| 4  | UInt32 | [ID](../identifiers.md) | Unique identifier | 1 |
| 8  | UInt32 | Data | Option or coordinate of the action | 10 |
| 12 | UInt16 | [Event](#npc-event-type) | How to process the message | 0 |
| 14 | UInt16 | [Role](../../constants/roletype.md) | The RoleType of the NPC | 0 |

#### NPC Event Type

☑️ Assumed (Soul)

🔶 Response data

| Val | Name | Description | Recipient | ID | Data |
|:------|:--------|:--------|:--------|:--------|:--------|
| 0 | ACTIVATE | Activates an NPC for dialog | Server | [NPC ID](../identifiers.md) | Dialog option |
| 1 | ADD_NPC | Adds an NPC to the map | Server | [NPC ID](../identifiers.md) | |
| 2 | LEAVE_MAP | Deletes an NPC from the map | Client | [NPC ID](../identifiers.md) | |
| 3 | DEL_NPC | Requests an NPC be deleted | Server | [NPC ID](../identifiers.md) | |
| 4 | CHANGE_POS | Change the position of the NPC | Both | [NPC ID](../identifiers.md) | `LOW:` X `HIGH:` Y 🔶 |
| 5 | LAY_NPC | Notifies the client to start placing | Client | | [Lookface](../../constants/lookface.md) |