# MsgAction

This message is received by the game server or game client as a general action request. The server responds to MsgAction with either a specific action message (such as a spawn that was missing or with item details) or with the MsgAction message itself (such as for the login messages). The client may or may not respond with the MsgAction in response to a server MsgAction message. 

MsgAction is used for a variety of actions, such as configuring the client during login, changing maps, requesting inventory and friends lists, setting the hero's location on login, jumping, and more.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5017](#patch-5017)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 28 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1010 |
| 4  | UInt32 | [System Time](../timestamp.md) | Milliseconds of system uptime | 1579535985 |
| 8  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 12 | UInt16 | X | X coordinate of the action or hero | 320 |
| 14 | UInt16 | Y | Y coordinate of the action or hero | 460 |
| 16 | UInt32 | [Direction](../../algorithms/calculations/direction.md) | Action direction | 0 |
| 20 | UInt32 | Data | Payload or target identifier | 0 |
| 24 | UInt32 | [Action](#action-type) | How to process the message | 0 | 

#### Action Type

☑️ Assumed (Soul)

🔶 Response data

| Val | Name | Description | Recipient | ID | Data |
|:------|:--------|:--------|:--------|:--------|:--------|
| 124 | CHANGE_DIR | Change facing direction | Server | [Hero ID](../identifiers.md) |  |
| 126 | CHANGE_EMOTION | Change emoting action | Server | [Hero ID](../identifiers.md) | [Action](../../constants/actions.md) |
| 130 | CHANGE_MAP | Change map (portal) | Server | [Hero ID](../identifiers.md) | |
| 137 | ENTER_MAP | Request hero location | Server | [Hero ID](../identifiers.md) | Map ID 🔶 |
| 138 | GET_ITEMS | Load items on login | Server | [Hero ID](../identifiers.md) | |
| 139 | GET_FRIENDS | Load friends on login | Server | [Hero ID](../identifiers.md) | |
| 141 | LEAVE_MAP | Remove role entity from map | Client | [Role ID](../identifiers.md) | |
| 142 | JUMP | Role entity jump | Server | [Role ID](../identifiers.md) | `LOW:` X `HIGH:` Y |
| 146 | UP_LEVEL | Notify new level | Server | [Hero ID](../identifiers.md) | |
| 147 | XP_CLEAR | Notify clear XP | Server | [Hero ID](../identifiers.md) |  |
| 148 | REVIVE | Request revive | Server | [Hero ID](../identifiers.md) | |
| 149 | DEL_ROLE | Delete hero | Server | [Hero ID](../identifiers.md) | |
| 150 | GET_WEAPON_SKILLS | Load skills on login | Server | [Hero ID](../identifiers.md) | |
| 151 | GET_MAGIC | Load spells on login | Server | [Hero ID](../identifiers.md) | |
| 152 | SET_PK_MODE | Set PK mode | Server | [Hero ID](../identifiers.md) | [Mode](../../constants/pkmode.md) |
| 153 | GET_SYN_ATTR | Get guild info | Server | [Hero ID](../identifiers.md) | |
| 154 | GHOST | Notify death | Server | [Hero ID](../identifiers.md) | |
| 155 | SYNCHRO | Synchronize screen | Server | [Hero ID](../identifiers.md) | |
| 156 | QUERY_FRIEND_INFO | Get friend info | Server | [Hero ID](../identifiers.md) | [Target ID](../identifiERS.md) |
| 157 | QUERY_LEAVE_WORD | Get offline messages | Server | [Hero ID](../identifiers.md) | |
| 158 | CHANGE_FACE | Change teammate or own avatar | Both | [Hero ID](../identifiers.md) | Face |
| 159 | MINE | Mine with pickaxe | Server | [Hero ID](../identifiers.md) | |
| 160 | TEAM_MEMBER_POS | Teammate position | Client | [Hero ID](../identifiers.md) | `LOW:` X `HIGH:` Y |
| 161 | QUERY_PLAYER | Get player spawn | Server | [Hero ID](../identifiers.md) | |
| 162 | ABORT_MAGIC | Cancel magic or chargeup | Server | [Hero ID](../identifiers.md) | |
| 164 | MAP_ARGB | Set game map ARGB | Client | | ARGB |
| 166 | QUERY_MEMBER | Get team member info | Server | [Hero ID](../identifiers.md) | [Target ID](../identifiers.md) |
| 167 | CREATE_BOOTH | Create market booth | Both | [Hero ID](../identifiers.md) | `LOW:` X `HIGH:` Y |
| 168 | SUSPEND_BOOTH | Pause market booth (unused) | Server | [Hero ID](../identifiers.md) | |
| 169 | RESUME_BOOTH | Resume market booth | Both | [Hero ID](../identifiers.md) | `LOW:` X `HIGH:` Y |
| 170 | DESTROY_BOOTH | Remove market booth | Server | [Hero ID](../identifiers.md) | |
| 172 | POST_CMD | Run client command | Client | [Hero ID](../identifiers.md) | Command |
| 173 | QUERY_EQUIPMENT | Get player's equipment | Server | [Hero ID](../identifiers.md) | |
| 174 | ABORT_TRANSFORM | Cancel transformation | Server | [Hero ID](../identifiers.md) | |
| 176 | LANDING | Cancel flight | Server | [Hero ID](../identifiers.md) | |
| 177 | GET_MONEY | Pick up money | Client | [Hero ID](../identifiers.md) | Amount |
| 179 | ENEMY_INFO | Get enemy info | Server | [Hero ID](../identifiers.md) | |
| 181 | KICKBACK | Rubberband to coord | Client | [Hero ID](../identifiers.md) | `LOW:` X `HIGH:` Y |
| 182 | DROP_MAGIC | Remove magic type | Client | [Hero ID](../identifiers.md) | [Magic Type](../../files/content/magictype.dat.md) |
| 183 | DROP_SKILL | Remove weapon skill | Client | [Hero ID](../identifiers.md) | [Weapon Skill Type](../../files/content/weaponskillname.ini.md) |
| 184 | SOUND_EFFECT | Monster sound at coord | Client | [Hero ID](../identifiers.md) | [Monster Type](../../files/content/monstertype.dat.md) |
| 186 | POST_DIALOG | Open a dialog window | Client | [Hero ID](../identifiers.md) | Dialog ID |

## Patch 5017

#### Message Definition

☑️ Assumed (Observed) - Redux

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 24 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1010 |
| 4  | UInt32 | [System Time](../timestamp.md) | Milliseconds of system uptime | 1579535985 |
| 8  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 12 | UInt32 | Data | Payload or target identifier | 0 |
| 16 | UInt16 | X | X coordinate of the action or hero | 320 |
| 18 | UInt16 | Y | Y coordinate of the action or hero | 460 |
| 20 | UInt16 | [Direction](../../algorithms/calculations/direction.md) | Action direction | 0 |
| 22 | UInt16 | [Action](#action-type) | How to process the message | 0 |

#### Action Type

☑️ Assumed (Observed) - COPSv6

🔶 Response data

| Val | Name | Description | Recipient | ID | Data |
|:------|:--------|:--------|:--------|:--------|:--------|
| 74 | GET_POSITION | Request hero location | Server | [Hero ID](../identifiers.md) | Map ID 🔶 |
| 75 | GET_ITEMS | Load items on login | Server | [Hero ID](../identifiers.md) | |
| 76 | GET_FRIENDS | Load friends on login | Server | [Hero ID](../identifiers.md) | |
| 77 | GET_WEAPON_SKILLS | Load skills on login | Server | [Hero ID](../identifiers.md) | |
| 78 | GET_MAGIC | Load spells on login | Server | [Hero ID](../identifiers.md) | |
| 79 | CHANGE_DIR | Change facing direction | Server | [Hero ID](../identifiers.md) |  |
| 81 | CHANGE_EMOTION | Change emoting action | Server | [Hero ID](../identifiers.md) | Emotion |
| 85 | CHANGE_MAP | Change map (portal) | Server | [Hero ID](../identifiers.md) | |
| 86 | ENTER_MAP | Add entity to map | Server | [Role ID](../identifiers.md) | Map ID |
| 92 | UP_LEVEL | Notify new level | Server | [Hero ID](../identifiers.md) | |
| 93 | XP_CLEAR | Notify clear XP | Server | [Hero ID](../identifiers.md) | |
| 94 | REVIVE | Request revive | Server | [Hero ID](../identifiers.md) | |
| 95 | DEL_ROLE | Delete hero | Server | [Hero ID](../identifiers.md) | |
| 96 | SET_PK_MODE | Set PK mode | Server | [Hero ID](../identifiers.md) | [Mode](../../constants/pkmode.md) |
| 97 | GET_SYN_ATTR | Get guild info | Server | [Hero ID](../identifiers.md) | |
| 99 | MINE | Mine with pickaxe | Server | [Hero ID](../identifiers.md) | |
| 101 | TEAM_LEAD_POS | Get team leader position | Client | [Hero ID](../identifiers.md) | [Game Map Type](../../files/content/gamemap.dat.md) |
| 102 | QUERY_PLAYER | Get player spawn | Server | [Hero ID](../identifiers.md) | |
| 104 | MAP_ARGB | Set game map ARGB | Client | | ARGB |
| 105 | QUERY_MEMBER | Get team member info | Server | [Hero ID](../identifiers.md) | [Target ID](../identifiers.md) |
| 106 | TEAM_MEMBER_POS | Teammate position | Client | [Hero ID](../identifiers.md) | `LOW:` X `HIGH:` Y |
| 108 | KICKBACK | Rubberband to coord | Client | [Hero ID](../identifiers.md) | `LOW:` X `HIGH:` Y |
| 109 | DROP_MAGIC | Remove magic type | Client | [Hero ID](../identifiers.md) | [Magic Type](../../files/content/magictype.dat.md) |
| 110 | DROP_SKILL | Remove weapon skill | Client | [Hero ID](../identifiers.md) | [Weapon Skill Type](../../files/content/weaponskillname.ini.md) |
| 111 | CREATE_BOOTH | Create market booth | Both | [Hero ID](../identifiers.md) | `LOW:` X `HIGH:` Y |
| 112 | SUSPEND_BOOTH | Pause market booth (unused) | Server | [Hero ID](../identifiers.md) | |
| 113 | RESUME_BOOTH | Resume market booth | Both | [Hero ID](../identifiers.md) | `LOW:` X `HIGH:` Y |
| 114 | DESTROY_BOOTH | Remove market booth | Server | [Hero ID](../identifiers.md) | |
| 116 | POST_CMD | Run client command | Client | [Hero ID](../identifiers.md) | Command |
| 117 | QUERY_EQUIPMENT | Get player's equipment | Server | [Hero ID](../identifiers.md) | |
| 118 | ABORT_TRANSFORM | Cancel transformation | Server | [Hero ID](../identifiers.md) | |
| 120 | LANDING | Cancel flight | Server | [Hero ID](../identifiers.md) | |
| 121 | GET_MONEY | Pick up money | Client | [Hero ID](../identifiers.md) | Amount |
| 123 | ENEMY_INFO | Get enemy info | Server | [Hero ID](../identifiers.md) | |
| 126 | POST_DIALOG | Open a dialog window | Client | [Hero ID](../identifiers.md) | Dialog ID |
| 130 | QUERY_LEAVE_WORD | Get offline messages | Server | [Hero ID](../identifiers.md) | |
| 132 | LEAVE_MAP | Remove role entity from map | Client | [Role ID](../identifiers.md) | |
| 133 | JUMP | Role entity jump | Server | [Role ID](../identifiers.md) | `LOW:` X `HIGH:` Y |
| 137 | GHOST | Notify death | Server | [Hero ID](../identifiers.md) | |
| 138 | SYNCHRO | Synchronize screen | Server | [Hero ID](../identifiers.md) | |
| 140 | QUERY_FRIEND_INFO | Get friend info | Server | [Hero ID](../identifiers.md) | [Target ID](../identifiERS.md) |
| 142 | CHANGE_FACE | Change teammate or own avatar | Both | [Hero ID](../identifiers.md) | Face |
| 162 | PATHFINDING | Trigger pathfinding to X, Y | Client | [Hero ID](../identifiers.md) | |
| 163 | ABORT_MAGIC | Cancel magic or chargeup | Server | [Hero ID](../identifiers.md) | |
