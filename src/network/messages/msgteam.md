# MsgTeam

This message performs simple team commands at the request of a client for managing the team and team members.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0 | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 8 |
| 2 | UInt16 | [MsgType](index.md#message-header) | Type of message | 1023 |
| 4 | UInt32 | [Action](#action-type) | The command being requested | 1 |
| 8 | UInt32 | Player | [Hero ID](/network/identifiers.md) of the target | 1000001 |

#### Action Type

☑️ Assumed (Soul)

```proto
enum TeamActionTypes {

    TEAM_ACTION_CREATE = 0;
    TEAM_ACTION_APPLY_JOIN = 1;
    TEAM_ACTION_LEAVE = 2;
    TEAM_ACTION_ACCEPT_INVITE = 3;
    TEAM_ACTION_INVITE = 4;
    TEAM_ACTION_ACCEPT_JOIN = 5;
    TEAM_ACTION_DISMISS = 6;
    TEAM_ACTION_KICK_OUT = 7;
    TEAM_ACTION_CLOSE_TEAM = 8;
    TEAM_ACTION_OPEN_TEAM = 9;
    TEAM_ACTION_CLOSE_MONEY_ACCESS = 10;
    TEAM_ACTION_OPEN_MONEY_ACCESS = 11;
    TEAM_ACTION_CLOSE_ITEM_ACCESS = 12;
    TEAM_ACTION_OPEN_ITEM_ACCESS = 13;
}
```
