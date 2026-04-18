# MsgUserAttrib

This message is sent by the game server to update one or more numeric user attributes in the game client. It can target the hero or another player on the game map.

Of the possibly attribute types, the user status attribute is one of the more complicated types. Statuses are a bitmap of effects that can be placed on a hero or entity, and are loaded from the [StatusEffect.ini](../../files/content/statuseffect.ini.md) file. Some examples of statuses found in the game include being poisoned, lucky, shielded, etc. They're also used for PK event haloes in later versions.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5017](#patch-5017)
* [Patch 5517](#patch-5517)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type                                   | Name                               | Description                         | Example   |
|:----|:---------------------------------------|:-----------------------------------|:------------------------------------|:----------|
| 0   | UInt16                                 | [MsgSize](index.md#message-header) | Size of the message                 | 24        |
| 2   | UInt16                                 | [MsgType](index.md#message-header) | Type of message                     | 1017      |
| 4   | UInt32                                 | [Hero ID](../identifiers.md)       | Unique identifier for the character | 1000000   |
| 8   | UInt32                                 | AttributeNum                       | Amount of attributes to update      | 1         |
| 12  | [UserAttrib](#userattrib-definition)[] | Attributes                         | Attributes list                     | See below |

#### UserAttrib Definition

☑️ Assumed (Soul)

| Type      | Name                           | Description                    | Example |
|:----------|:-------------------------------|:-------------------------------|:--------|
| UInt32    | [AttribType](#userattrib-type) | The attribute to update        | 2       |
| UInt32[2] | Data                           | The new value of the attribute | 10      |

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

| Pos | Type                                   | Name                               | Description                         | Example   |
|:----|:---------------------------------------|:-----------------------------------|:------------------------------------|:----------|
| 0   | UInt16                                 | [MsgSize](index.md#message-header) | Size of the message                 | 24        |
| 2   | UInt16                                 | [MsgType](index.md#message-header) | Type of message                     | 1017      |
| 4   | UInt32                                 | [Hero ID](../identifiers.md)       | Unique identifier for the character | 1000000   |
| 8   | UInt32                                 | AttributeNum                       | Amount of attributes to update      | 1         |
| 12  | [UserAttrib](#userattrib-definition)[] | Attributes                         | Attributes list                     | See below |

#### UserAttrib Definition

☑️ Assumed (Soul)

| Type      | Name                           | Description                    | Example |
|:----------|:-------------------------------|:-------------------------------|:--------|
| UInt32    | [AttribType](#userattrib-type) | The attribute to update        | 2       |
| UInt32[2] | Data                           | The new value of the attribute | 10      |

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

## Patch 5517

☑️ Assumed (Observed) - Reverse Engineering Client and Observing Client

#### Message Definition

| Pos | Type                                     | Name                               | Description                         | Example   |
|:----|:-----------------------------------------|:-----------------------------------|:------------------------------------|:----------|
| 0   | UInt16                                   | [MsgSize](index.md#message-header) | Size of the message                 | 52        |
| 2   | UInt16                                   | [MsgType](index.md#message-header) | Type of message                     | 10017     |
| 4   | UInt32                                   | [Hero ID](../identifiers.md)       | Unique identifier for the character | 1000000   |
| 8   | UInt32                                   | AttributeNum                       | Amount of attributes to update      | 1         |
| 12  | [UserAttrib](#userattrib-definition-1)[] | Attributes                         | Attributes list                     | See below |

#### UserAttrib Definition

| Pos (relative) | Type   | Name                             | Description                  | Example |
|:---------------|:-------|:---------------------------------|:-----------------------------|:--------|
| 0              | UInt32 | [AttribType](#userattrib-type-1) | The attribute to update      | 17      |
| 4              | UInt64 | Data1                            | Primary value for AttribType | 259200  |
| 12             | UInt64 | Data2                            | Secondary value              | 0       |

##### UserAttrib Type

```proto
enum UserAttribTypes {

    USERATTRIB_LIFE = 0;
    USERATTRIB_MAXLIFE = 1;
    USERATTRIB_MANA = 2;
    USERATTRIB_MAXMANA = 3;
    USERATTRIB_MONEY = 4;
    USERATTRIB_EXP = 5;
    USERATTRIB_PK_POINTS = 6;
    USERATTRIB_PROFESSION = 7;
    USERATTRIB_STAMINA = 8;
    USERATTRIB_WAREHOUSE_MONEY = 9;        // Warehouse Dialog (CDlgDepot) needs to be open (refreshes it)
    USERATTRIB_ADDPOINT = 10;              // Allocatable Attribute Points
    USERATTRIB_LOOK = 11;
    USERATTRIB_LEVEL = 12;
    USERATTRIB_SOUL = 13;                  // Spirit attribute points
    USERATTRIB_HEALTH = 14;                // Vitality attribute points
    USERATTRIB_FORCE = 15;                 // Strength attribute points
    USERATTRIB_SPEED = 16;                 // Agility attribute points
    USERATTRIB_BLESS_SECONDS = 17;         // Heaven blessing remaining seconds
    USERATTRIB_DOUBLE_XP_SECONDS = 18;
    USERATTRIB_SYN_DONATION = 19;          // Guild Donation
    USERATTRIB_CURSE_SECONDS = 20;         // No XP Gain & Prevent City Teleport Scrolls remaining seconds
    USERATTRIB_METEMPSYCHOSIS = 22;        // Rebirth Count
    USERATTRIB_UNKNOWN_1 = 23;
    USERATTRIB_USERSTATUS = 25;            // 128-bit status bitwise flag: Data1=bits 0-63, Data2=bits 64-127 See: UserStatusFlags
    USERATTRIB_HAIR = 26;
    USERATTRIB_XP_CIRCLE = 27;             // XP Skill Circle % (0-100)
    USERATTRIB_LUCKY_SECONDS = 28;         // Lucky time remaining milliseconds
    USERATTRIB_EMONEY = 29;                // Conquer Points
    USERATTRIB_UNKNOWN_2 = 30;
    USERATTRIB_ONLINE_TRAINING = 31;       // Online training state See: UserAttribOnlineTrainingState
    USERATTRIB_ENTHRALLMENT_UPDATE_STATE = 32;
    USERATTRIB_ENTHRALLMENT_ONLINE_TIME_SYNC = 33;
    USERATTRIB_ENTHRALLMENT_OFFLINE_TIME_SYNC = 34;
    USERATTRIB_ENTHRALLMENT_RESET = 35;
    USERATTRIB_EXTRA_BATTLE_POWER = 36;
    USERATTRIB_MENTOR_LEVEL = 37;
    USERATTRIB_MERCHANT = 38;
    USERATTRIB_VIP_LEVEL = 39;
    USERATTRIB_QUIZ_POINTS = 40;
    USERATTRIB_ENLIGHT_POINTS = 41;
    USERATTRIB_HONOR_POINTS = 42;
    USERATTRIB_DOUBLE_ARENA_PARTNER_HP = 43; // Arena Partner's HP in a double arena match
    USERATTRIB_GUILD_BP = 44;
    USERATTRIB_BOUND_EMONEY = 45;            // Bound Conquer Points
    USERATTRIB_HORSE_RACING_POINTS = 47;
    USERATTRIB_UNKNOWN_3 = 48;
    USERATTRIB_AZURE_SHIELD = 49;            // See: AzureShieldSubType
    USERATTRIB_FIR_METE_PROF = 50;           // Profession during first rebirth
    USERATTRIB_BIRTH_PROF = 51;              // Original Profession
    USERATTRIB_TEAM_ID = 52;                 // PK Team / Arena Team ID
    USERATTRIB_SOUL_SHACKLE = 54;            // Stops player from reviving
    USERATTRIB_UNKNOWN_4 = 128;
}
```

#### UserAttrib Special Values

```proto
enum AzureShieldSubType {
    // USERATTRIB_AZURE_SHIELD.
    // Data1 Low = Type (93/113) High = Timer (Seconds)
    // Data2 Low = Reduction Percentage Data2 High = Shield Level
    AZURE_SHIELD_ACTIVE = 93;
    AZURE_SHIELD_BLOCK  = 113;
}
```

```proto
enum UserStatusFlags {
    // USERATTRIB_USERSTATUS Data1 (bits 0-63) Flags
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
    USERSTATUS_CYCLONE = 0x00800000;
    USERSTATUS_DODGE = 0x04000000;
    USERSTATUS_FLY = 0x08000000;
    USERSTATUS_CAST_PRAY = 0x40000000;
    USERSTATUS_PRAYING = 0x80000000;
    USERSTATUS_HEAVEN_BLESS = 0x200000000;
}

enum UserStatusFlagsData2 {
    // USERATTRIB_USERSTATUS Data2 (bits 64-127)
    USERSTATUS_TYRANT_AURA = 0x400000000;        // Tyrant - increases critical strike
    USERSTATUS_FEND_AURA = 0x1000000000;         // Fend - increases immunity
    USERSTATUS_METAL_AURA = 0x4000000000;        // Elemental Aura - Metal Resistance
    USERSTATUS_WOOD_AURA = 0x10000000000;        // Elemental Aura - Wood Resistance
    USERSTATUS_WATER_AURA = 0x40000000000;       // Elemental Aura - Water Resistance
    USERSTATUS_FIRE_AURA = 0x100000000000;       // Elemental Aura - Fire Resistance
    USERSTATUS_EARTH_AURA = 0x400000000000;      // Elemental Aura - Earth Resistance
}
```

```proto
enum UserAttribOnlineTrainingState {
    // USERATTRIB_ONLINE_TRAINING
    ONLINE_TRAINING_START = 0;
    ONLINE_TRAINING_ACTIVE = 1;
    ONLINE_TRAINING_READY = 2;
    ONLINE_TRAINING_ADD_POINTS = 3;
    ONLINE_TRAINING_COLLECTING = 4; // Status Icon Animation
    ONLINE_TRAINING_END = 5;
}
```