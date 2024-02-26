# MsgUserAttrib

This message is sent by the game server to update one or more numeric user attributes in the game client. It can target the hero or another player on the game map.

Of the possibly attribute types, the user status attribute is one of the more complicated types. Statuses are a bitmap of effects that can be placed on a hero or entity, and are loaded from the [StatusEffect.ini](/files/content/statuseffect.ini.md) file. Some examples of statuses found in the game include being poisoned, lucky, shielded, etc. They're also used for PK event haloes in later versions.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5017](#patch-5017)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 24 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1017 |
| 4  | UInt32 | [Hero ID](/network/identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | UInt32 | AttributeNum | Amount of attributes to update | 1 |
| 12 | [UserAttrib](#userattrib-definition)[] | Attributes | Attributes list | See below |

#### UserAttrib Definition

☑️ Assumed (Soul)

| Type | Name | Description | Example |
|:--------|:--------|:--------|:--------|
| UInt32 | [AttribType](#userattrib-type) | The attribute to update | 2 | 
| UInt32[2] | Data | The new value of the attribute | 10 |

#### UserAttrib Type

☑️ Assumed (Observed) - CoFuture

```proto
enum UserAttribTypes {

    USERATTRIB_LIFE = 0;
    USERATTRIB_MAXLIFE = 1;
    USERATTRIB_MANA = 2;
    USERATTRIB_MAXMANA = 3;
    USERATTRIB_MONEY = 4;
    USERATTRIB_EXP = 5;
    USERATTRIB_PK = 6;
    USERATTRIB_PROFESSION = 7;
    USERATTRIB_SIZE_ADD = 8;
    USERATTRIB_PP = 9;
    USERATTRIB_ADDPOINT = 11;
    USERATTRIB_LOOK = 12;
    USERATTRIB_LEV = 13;
    USERATTRIB_SOUL = 14;
    USERATTRIB_HEALTH = 15;
    USERATTRIB_FORCE = 16;
    USERATTRIB_SPEED = 17;
    USERATTRIB_BLESS_SECONDS = 18;
    USERATTRIB_DOUBLE_XP_SECONDS = 19;
    USERATTRIB_SYN_WAR_POLE = 20;
    USERATTRIB_CURSE_SECONDS = 21;
    USERATTRIB_TIME_ADD_SECONDS = 22;
    USERATTRIB_METEMPSYCHOSIS = 23;
    USERATTRIB_USERSTATUS = 26;
    USERATTRIB_HAIR = 27;
    USERATTRIB_XP = 28;
}
```

#### UserAttrib Special Values

☑️ Assumed (Observed) - COPSv6

```proto
enum UserAttribSizeAddFlags {

    USERATTRIB_SIZE_ADD_NONE = 0;
    USERATTRIB_SIZE_ADD_CURSED = 1;
    USERATTRIB_SIZE_ADD_BLESSED = 2;
}
```

```proto
enum UserStatusFlags {

    USERSTATUS_NORMAL = 0x00000000;
    USERSTATUS_FLASHING_NAME = 0x00000001;
    USERSTATUS_POISONED = 0x00000002;
    USERSTATUS_INVISIBLE = 0x00000004;
    USERSTATUS_XPFULL = 0x00000010;
    USERSTATUS_TEAM_LEADER = 0x00000040;
    USERSTATUS_ADJUST_DODGE = 0x00000080;
    USERSTATUS_SHIELD = 0x00000100;
    USERSTATUS_STIGMA = 0x00000200;
    USERSTATUS_GHOST = 0x00000400;
    USERSTATUS_DISAPPEARING = 0x00000800;
    USERSTATUS_RED_NAME = 0x00004000;
    USERSTATUS_BLACK_NAME = 0x00008000;
    USERSTATUS_SUPERMAN = 0x00040000;
    USERSTATUS_CYCLONE_ = 0x00800000;
    USERSTATUS_DODGE = 0x04000000;
    USERSTATUS_FLY = 0x08000000;
}
```

## Patch 5017

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 24 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1017 |
| 4  | UInt32 | [Hero ID](/network/identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | UInt32 | AttributeNum | Amount of attributes to update | 1 |
| 12 | [UserAttrib](#userattrib-definition)[] | Attributes | Attributes list | See below |

#### UserAttrib Definition

☑️ Assumed (Soul)

| Type | Name | Description | Example |
|:--------|:--------|:--------|:--------|
| UInt32 | [AttribType](#userattrib-type) | The attribute to update | 2 | 
| UInt32[2] | Data | The new value of the attribute | 10 |

#### UserAttrib Type

☑️ Assumed (Observed) - COPSv6

```proto
enum UserAttribTypes {

    USERATTRIB_LIFE = 0;
    USERATTRIB_MAXLIFE = 1;
    USERATTRIB_MANA = 2;
    USERATTRIB_MAXMANA = 3;
    USERATTRIB_MONEY = 4;
    USERATTRIB_EXP = 5;
    USERATTRIB_PK = 6;
    USERATTRIB_PROFESSION = 7;
    USERATTRIB_SIZE_ADD = 8;
    USERATTRIB_PP = 9;
    USERATTRIB_ADDPOINT = 11;
    USERATTRIB_LOOK = 12;
    USERATTRIB_LEV = 13;
    USERATTRIB_SOUL = 14;
    USERATTRIB_HEALTH = 15;
    USERATTRIB_FORCE = 16;
    USERATTRIB_SPEED = 17;
    USERATTRIB_BLESS_SECONDS = 18;
    USERATTRIB_DOUBLE_XP_SECONDS = 19;
    USERATTRIB_SYN_WAR_POLE = 20;
    USERATTRIB_CURSE_SECONDS = 21;
    USERATTRIB_TIME_ADD_SECONDS = 22;
    USERATTRIB_METEMPSYCHOSIS = 23;
    USERATTRIB_USERSTATUS = 26;
    USERATTRIB_HAIR = 27;
    USERATTRIB_LUCKY_SECONDS = 29;
    USERATTRIB_EMONEY = 30;
    USERATTRIB_XP = 31;
    USERATTRIB_OFFLINE_TRAINING_PROGRESS = 32;
}
```

#### UserAttrib Special Values

☑️ Assumed (Observed) - COPSv6

```proto
enum UserAttribSizeAddFlags {

    USERATTRIB_SIZE_ADD_NONE = 0;
    USERATTRIB_SIZE_ADD_CURSED = 1;
    USERATTRIB_SIZE_ADD_BLESSED = 2;
}
```

```proto
enum UserStatusFlags {

    USERSTATUS_NORMAL = 0x00000000;
    USERSTATUS_FLASHING_NAME = 0x00000001;
    USERSTATUS_POISONED = 0x00000002;
    USERSTATUS_INVISIBLE = 0x00000004;
    USERSTATUS_XPFULL = 0x00000010;
    USERSTATUS_TEAM_LEADER = 0x00000040;
    USERSTATUS_ADJUST_DODGE = 0x00000080;
    USERSTATUS_SHIELD = 0x00000100;
    USERSTATUS_STIGMA = 0x00000200;
    USERSTATUS_GHOST = 0x00000400;
    USERSTATUS_DISAPPEARING = 0x00000800;
    USERSTATUS_RED_NAME = 0x00004000;
    USERSTATUS_BLACK_NAME = 0x00008000;
    USERSTATUS_SUPERMAN = 0x00040000;
    USERSTATUS_CYCLONE_ = 0x00800000;
    USERSTATUS_DODGE = 0x04000000;
    USERSTATUS_FLY = 0x08000000;
    USERSTATUS_CAST_PRAY = 0x40000000;
    USERSTATUS_PRAYING = 0x80000000;
}
```
