# MsgSyndicate

This message is sent between the client and game server to request and respond to guild-related actions, such as joining and leaving a guild, managing allies and enemies, disbanding the guild, and more. Similar to [MsgAction](msgaction.md), the server responds to MsgSyndicate with either a specific action message (such as querying for the [MsgSyndicateAttributeInfo](msgsyndicateattributeinfo.md) message) or with the MsgSyndicate message itself (such as for applying for membership).

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 12 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1107 |
| 4  | UInt32 | [Action](#action-types) | Guild action being performed | 1 |
| 8  | UInt32 | Target | Target individual or guild identifier | 1000000 |

#### Action Types

☑️ Assumed (Observed) - CoFuture + Soul

🔶 Response data

| Val | Name | Description | Recipient | Target |
|:------|:--------|:--------|:--------|:--------|
| 1  | APPLY_JOIN | Apply to join a guild (sends INVITE_JOIN) | Server | [Target ID](/network/identifiers.md) |
| 2  | INVITE_JOIN | Invite a player to join a guild | Client | [Target ID](/network/identifiers.md) |
| 3  | LEAVE_SYN | Request to leave current guild | Server | |
| 4  | KICKOUT_MEMBER | Kick a member from guild | Client | [Target ID](/network/identifiers.md) |
| 6  | QUERY_SYN_NAME | Sends [MsgName](msgname.md) with guild name | Server | Syndicate ID |
| 7  | ALLY_APPLY | Sets a guild as an ally | Server | Ally's Syndicate ID |
| 8  | CLEAR_ALLY | Removes an ally guild | Server | Ally's Syndicate ID |
| 9  | ANTAGONIZE | Sets a guild as an enemy | Server | Enemy's Syndicate ID |
| 10 | CLEAR_ANTAGONIZE | Removes an enemy guild | Server | Enemy's Syndicate ID |
| 11 | DONATE_MONEY | Add silver to the guild fund | Server | Amount |
| 12 | QUERY_SYNATTR | Query for guild attributes | Server | [Target ID](/network/identifiers.md) |
| 14 | SET_SYN | Sent on login to set syndicate ID | Client | Syndicate ID |
| 19 | DESTROY_SYN | Terminates a guild | Client | Syndicate ID |