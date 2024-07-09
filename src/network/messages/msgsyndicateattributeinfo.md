# MsgSyndicateAttributeInfo

This game server message is sent to the client to display details about a guild and the player's role and donations in that guild. In later versions of the client, this expanded to include other donation types, guild player requirements, how long the player has been enrolled in the guild for, etc.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5517](#patch-5517)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - CoFuture + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 40 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1106 |
| 4  | UInt32 | Syndicate ID | [Unique identifier](/network/identifiers.md) of the player | 1000000 |
| 8  | UInt32 | Proffer | Silver amount offered as donation | 10000 |
| 12 | UInt32 | Fund | Total silver fund | 10000 |
| 16 | UInt32 | Population | Number of guild members | 1 |
| 20 | Byte | [Rank](#syndicate-rank) | Position in the guild | 100 |
| 21 | Char[16] | Leader | Name of the guild leader | Player |

#### Syndicate Rank

☑️ Assumed (Observed) - CoFuture

```proto
enum SyndicateRank {

    SYNDICATE_RANK_MEMBER = 50;
    SYNDICATE_RANK_DEPUTY_LEADER = 90;
    SYNDICATE_RANK_LEADER = 100;
}
```

## Patch 5517

#### Message Definition

🚩 Incomplete

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 92 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1106 |
| 4  | UInt32 | Syndicate ID | [Unique identifier](/network/identifiers.md) of the player | 1000000 |
| 8  | UInt32 | Proffer | Silver amount offered as donation | 10000 |
| 12 | UInt64 | Fund | Total silver fund | 10000 |
| 20 | UInt32 | EMoney Fund | Total CPs fund | 0 |
| 24 | UInt32 | Population | Number of guild members | 1 |
| 28 | Byte | [Rank](#syndicate-rank-1) | Position in the guild | 100 |
| 32 | Char[16] | Leader | Name of the guild leader | Player |
| 48 | UInt32 | Level Req | Required minimum level for joining | 1 |
| 52 | UInt32 | Metempsychosis Req | Required minimum rebirth for joining | 1 |
| 56 | UInt32 | Profession Req | Required professions for joining as a bitmap | 0 |
| 60 | UInt32 | Level | Overall guild level | 1 |
| 67 | UInt32 | Registration Date | Day the guild was registered on in YYYYMMDD | 20150116 |

#### Syndicate Rank

🚩 Incomplete

```proto
enum SyndicateRank {

    SYNDICATE_RANK_AGENT = 590,
    SYNDICATE_RANK_AIDE = 0X25A,
    SYNDICATE_RANK_ARSENAL_AGENT = 0X254,
    SYNDICATE_RANK_ARS_FOLLOWER = 0X1F0,
    SYNDICATE_RANK_A_SUPERVISOR = 0X358,
    SYNDICATE_RANK_CP_AGENT = 0X255,
    SYNDICATE_RANK_CP_FOLLOWER = 0X1F1,
    SYNDICATE_RANK_CP_SUPERVISOR = 0X359,
    SYNDICATE_RANK_DEPUTY_LEADER = 990,
    SYNDICATE_RANK_DEPUTY_STEWARD = 650,
    SYNDICATE_RANK_D_LEADER_AIDE = 0X263,
    SYNDICATE_RANK_D_LEADER_SPOUSE = 620,
    SYNDICATE_RANK_FOLLOWER = 490,
    SYNDICATE_RANK_G_SUPERVISOR = 0X356,
    SYNDICATE_RANK_GUIDE_AGENT = 0X252,
    SYNDICATE_RANK_GUIDE_FOLLOWER = 0X1EE,
    SYNDICATE_RANK_GUILD_LEADER = 0X3E8,
    SYNDICATE_RANK_H_DEPUTY_LEADER = 980,
    SYNDICATE_RANK_HONORARY_MANAGER = 880,
    SYNDICATE_RANK_HONORARY_STEWARD = 680,
    SYNDICATE_RANK_HONORARY_SUPERV = 840,
    SYNDICATE_RANK_LEADER_SPOUSE = 920,
    SYNDICATE_RANK_LILY_AGENT = 0X24F,
    SYNDICATE_RANK_LILY_FOLLOWER = 0X1EB,
    SYNDICATE_RANK_LILY_SUPERVISOR = 0X353,
    SYNDICATE_RANK_L_SPOUSE_AIDE = 610,
    SYNDICATE_RANK_MANAGER = 890,
    SYNDICATE_RANK_MANAGER_AIDE = 510,
    SYNDICATE_RANK_MANAGER_SPOUSE = 520,
    SYNDICATE_RANK_MEMBER = 200,
    SYNDICATE_RANK_NONE = 0,
    SYNDICATE_RANK_ORCHID_AGENT = 0X256,
    SYNDICATE_RANK_ORCHID_FOLLOWER = 0X1F2,
    SYNDICATE_RANK_O_SUPERVISOR = 0X35A,
    SYNDICATE_RANK_PK_AGENT = 0X251,
    SYNDICATE_RANK_PK_FOLLOWER = 0X1ED,
    SYNDICATE_RANK_PK_SUPERVISOR = 0X355,
    SYNDICATE_RANK_ROSE_AGENT = 0X250,
    SYNDICATE_RANK_ROSE_FOLLOWER = 0X1EC,
    SYNDICATE_RANK_ROSE_SUPERVISOR = 0X354,
    SYNDICATE_RANK_SENIOR_MEMBER = 210,
    SYNDICATE_RANK_SILVER_AGENT = 0X253,
    SYNDICATE_RANK_SILVER_FOLLOWER = 0X1EF,
    SYNDICATE_RANK_S_SUPERVISOR = 0X357,
    SYNDICATE_RANK_STEWARD = 690,
    SYNDICATE_RANK_STEWARD_SPOUSE = 420,
    SYNDICATE_RANK_SUPERVISOR = 850,
    SYNDICATE_RANK_SUPERVISOR_AIDE = 0X1FF,
    SYNDICATE_RANK_SUPERV_SPOUSE = 0X209,
    SYNDICATE_RANK_T_SUPERVISOR = 0X35B,
    SYNDICATE_RANK_TULIP_AGENT = 0X257,
    SYNDICATE_RANK_TULIP_FOLLOWER = 0X1F3
}
```

#### Profession Requirement Bitmap

❓ Unverified

```proto
enum SyndicateProfessionRequirementFlags {

    SYNDICATE_PROFESSION_REQ_NONE = 0x00000000;
    SYNDICATE_PROFESSION_REQ_TROJAN = 0x00000001;
    SYNDICATE_PROFESSION_REQ_WARRIOR = 0x00000002;
    SYNDICATE_PROFESSION_REQ_TAOIST = 0x00000004;
    SYNDICATE_PROFESSION_REQ_ARCHER = 0x00000008;
    SYNDICATE_PROFESSION_REQ_NINJA = 0x00000010;
    SYNDICATE_PROFESSION_REQ_MONK = 0x00000020;
}
```
