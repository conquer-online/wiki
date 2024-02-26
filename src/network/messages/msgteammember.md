# MsgTeamMember

This message is sent to the client to update the team member list. It can include one or more team members, but each message must be all additions or all removals. Visually in the client, this is the vertical list of members' faces and healths along the right side of the screen.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:----|:--------|:--------|:--------|:--------|
| 0 | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 34 |
| 2 | UInt16 | [MsgType](index.md#message-header) | Type of message | 1026 |
| 4 | Byte | [Action](#team-member-action-type) | Adding or removing | 1 |
| 5 | Byte | Amount | Number of team members being acted upon | 1 |
| 6 | [TeamMember](#team-member-definition) | Members | Repeated list of team members | |

#### Team Member Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:----|:--------|:--------|:--------|:--------|
| 0 | Char[16] | Name | Hero name | Player |
| 16 | UInt32 | ID | [Hero ID](/network/identifiers.md) of the member | 1000001 |
| 20 | UInt32 | [Look Face](/constants/lookface.md) | Mesh of the entity | 501002 |
| 24 | UInt16 | Max HP | Total HP the member can have | 92 |
| 26 | UInt16 | HP | Total HP the member has | 54 |

#### Team Member Action Type

☑️ Assumed (Soul)

```proto
enum TeamMemberActionTypes {

    TEAM_MEMBER_ACTION_ADD_MEMBER = 0;
    TEAM_MEMBER_ACTION_DROP_MEMBER = 1;
}
```
