# MsgTalk

This message is sent from the game client to send a message to other players, or sent from the game server to receive a message from another player. Messages can also originate from the server as `SYSTEM` and be can be addressed to `ALLUSERS` for messages sent to all players. 

The following text messages can be sent by the game server to control the client before sign-on completes.

* __NEW_ROLE__ (Login attribute): Opens the character creation screen after receiving [MsgConnect](msgconnect.md).
* __ANSWER_OK__ (Login / Register attribute): Character was created or the character exists.

__Text attributes__ are used to control where the message appears in the client. For example, the text channel it appears in, as a system message in the top left corner, an announcement across the screen, etc. __Text styles__ can also be used to add flare to messages; however, Conquer Online doesn't use this.

When constructing the string packer, character names remain the same length (max 16 characters). The max length for a message is 256 characters, and the max emotion is 16 characters.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 4354](#patch-4354)
* [Patch 5615](#patch-5615)
* [Patch 5808](#patch-5808)

## Patch 4267

#### Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 42 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1004 |
| 4  | Int32 | Text Color | [ARGB32](https://en.wikipedia.org/wiki/RGBA_color_model) color of the text | 00FF0000 |
| 8  | UInt16 | [Text Attribute](#text-attribute) | Defines where the text appears | 2000 |
| 10 | Uint16 | [Text Style](#text-style) | Defines how the text appears | 0 |
| 12 | UInt32 | [Local Time](/network/timestamp.md) | Hours and minutes | 1241 |
| 16 | [NetStringPacker](/network/stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Speaker | Author of the message | SYSTEM |
| Header | Recipient of the message | ALLUSERS |
| Emotion | A prefix to the message | |
| Words | The body of the message | Testing |


#### Text Attribute

☑️ Assumed (Observed) - Comet

```proto
enum TextAttribute {

    TXTATTRIB_UNSPECIFIED = 0;
    TXTATTRIB_NORMAL = 2000;
    TXTATTRIB_WHISPER = 2001;
    TXTATTRIB_ACTION = 2002;
    TXTATTRIB_TEAM = 2003;
    TXTATTRIB_SYNDICATE = 2004;
    TXTATTRIB_FAMILY = 2006;
    TXTATTRIB_SYSTEM = 2007;
    TXTATTRIB_YELL = 2008;
    TXTATTRIB_FRIEND = 2009;
    TXTATTRIB_GM = 2011;
    TXTATTRIB_NOTIFICATION = 2012;
    TXTATTRIB_GHOST = 2013;
    TXTATTRIB_SERVICE = 2014;
    TXTATTRIB_TIP = 2015;

    TXTATTRIB_REGISTER = 2100;
    TXTATTRIB_LOGIN = 2101;
    TXTATTRIB_SHOP = 2102;
    TXTATTRIB_PET = 2103;
    TXTATTRIB_VENDOR = 2104;
    TXTATTRIB_WEBPAGE = 2105;
    TXTATTRIB_SYNWAR_FIRST = 2108;
    TXTATTRIB_SYNWAR_NEXT = 2109;
    TXTATTRIB_LEAVE_WORD = 2110;
    TXTATTRIB_SYNANNOUNCE = 2111;

    TXTATTRIB_TRADE_BOARD = 2201;
    TXTATTRIB_FRIEND_BOARD = 2202;
    TXTATTRIB_TEAM_BOARD = 2203;
    TXTATTRIB_SYN_BOARD = 2204;
    TXTATTRIB_OTHER_BOARD = 2205;
}
```

#### Text Style

☑️ Assumed (Observed) - Comet

```proto
enum TextStyle {

    TXTSTYLE_NORMAL = 0;
    TXTSTYLE_SCROLL = 0x01;
    TXTSTYLE_FLASH = 0x02;
    TXTSTYLE_BLAST = 0x08;
}
```

## Patch 4354

#### Message Definition

☑️ Assumed (Observed) - Comet

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 50 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1004 |
| 4  | Int32 | Text Color | [ARGB32](https://en.wikipedia.org/wiki/RGBA_color_model) color of the text | 00FF0000 |
| 8  | UInt16 | [Text Attribute](#text-attribute-1) | Defines where the text appears | 2000 |
| 10 | Uint16 | [Text Style](#text-style-1) | Defines how the text appears | 0 |
| 12 | UInt32 | [Local Time](/network/timestamp.md) | Hours and minutes | 1241 |
| 16 | UInt32 | Hearer [View](/algorithms/calculations/roleview.md) | Character view mesh for the hearer | 501002 |
| 20 | UInt32 | Speaker [View](/algorithms/calculations/roleview.md) | Character view mesh for the speaker | 501002 |
| 24 | [NetStringPacker](/network/stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Speaker | Author of the message | SYSTEM |
| Header | Recipient of the message | ALLUSERS |
| Emotion | A prefix to the message | |
| Words | The body of the message | Testing |

#### Text Attribute

☑️ Assumed (Observed) - Comet

```proto
enum TextAttribute {

    TXTATTRIB_UNSPECIFIED = 0;
    TXTATTRIB_NORMAL = 2000;
    TXTATTRIB_WHISPER = 2001;
    TXTATTRIB_ACTION = 2002;
    TXTATTRIB_TEAM = 2003;
    TXTATTRIB_SYNDICATE = 2004;
    TXTATTRIB_FAMILY = 2006;
    TXTATTRIB_SYSTEM = 2007;
    TXTATTRIB_YELL = 2008;
    TXTATTRIB_FRIEND = 2009;
    TXTATTRIB_GM = 2011;
    TXTATTRIB_NOTIFICATION = 2012;
    TXTATTRIB_GHOST = 2013;
    TXTATTRIB_SERVICE = 2014;
    TXTATTRIB_TIP = 2015;

    TXTATTRIB_REGISTER = 2100;
    TXTATTRIB_LOGIN = 2101;
    TXTATTRIB_SHOP = 2102;
    TXTATTRIB_PET = 2103;
    TXTATTRIB_VENDOR = 2104;
    TXTATTRIB_WEBPAGE = 2105;
    TXTATTRIB_SYNWAR_FIRST = 2108;
    TXTATTRIB_SYNWAR_NEXT = 2109;
    TXTATTRIB_LEAVE_WORD = 2110;
    TXTATTRIB_SYNANNOUNCE = 2111;

    TXTATTRIB_TRADE_BOARD = 2201;
    TXTATTRIB_FRIEND_BOARD = 2202;
    TXTATTRIB_TEAM_BOARD = 2203;
    TXTATTRIB_SYN_BOARD = 2204;
    TXTATTRIB_OTHER_BOARD = 2205;

    TXTATTRIB_BROADCAST = 2500;
}
```

#### Text Style

☑️ Assumed (Observed) - Comet

```proto
enum TextStyle {

    TXTSTYLE_NORMAL = 0;
    TXTSTYLE_SCROLL = 0x01;
    TXTSTYLE_FLASH = 0x02;
    TXTSTYLE_BLAST = 0x08;
}
```

## Patch 5615

#### Message Definition

☑️ Assumed (Observed) - Chimera

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 52 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1004 |
| 4  | Int32 | Text Color | [ARGB32](https://en.wikipedia.org/wiki/RGBA_color_model) color of the text | 00FF0000 |
| 8  | UInt16 | [Text Attribute](#text-attribute-2) | Defines where the text appears | 2000 |
| 10 | Uint16 | [Text Style](#text-style-2) | Defines how the text appears | 0 |
| 12 | UInt32 | [Local Time](/network/timestamp.md) | Hours and minutes | 1241 |
| 16 | UInt32 | Hearer [View](/algorithms/calculations/roleview.md) | Character view mesh for the hearer | 501002 |
| 20 | UInt32 | Speaker [View](/algorithms/calculations/roleview.md) | Character view mesh for the speaker | 501002 |
| 24 | [NetStringPacker](/network/stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Speaker | Author of the message | SYSTEM |
| Header | Recipient of the message | ALLUSERS |
| Emotion | A prefix to the message | |
| Words | The body of the message | Testing |
| Unknown | Not referenced in the client assembly | |
| Unknown | Not referenced in the client assembly | |

#### Text Attribute

☑️ Assumed (Observed) - Chimera

```proto
enum TextAttribute {

    TXTATTRIB_UNSPECIFIED = 0;
    TXTATTRIB_NORMAL = 2000;
    TXTATTRIB_WHISPER = 2001;
    TXTATTRIB_ACTION = 2002;
    TXTATTRIB_TEAM = 2003;
    TXTATTRIB_SYNDICATE = 2004;
    TXTATTRIB_FAMILY = 2006;
    TXTATTRIB_SYSTEM = 2007;
    TXTATTRIB_YELL = 2008;
    TXTATTRIB_FRIEND = 2009;
    TXTATTRIB_GM = 2011;
    TXTATTRIB_NOTIFICATION = 2012;
    TXTATTRIB_GHOST = 2013;
    TXTATTRIB_SERVICE = 2014;
    TXTATTRIB_TIP = 2015;
    TXTATTRIB_WORLD = 2021,
    TXTATTRIB_QUALIFIER = 2022,
    TXTATTRIB_STUDY = 2024,

    TXTATTRIB_REGISTER = 2100;
    TXTATTRIB_LOGIN = 2101;
    TXTATTRIB_SHOP = 2102;
    TXTATTRIB_PET = 2103;
    TXTATTRIB_VENDOR = 2104;
    TXTATTRIB_WEBPAGE = 2105;
    TXTATTRIB_SYNWAR_FIRST = 2108;
    TXTATTRIB_SYNWAR_NEXT = 2109;
    TXTATTRIB_LEAVE_WORD = 2110;
    TXTATTRIB_SYNANNOUNCE = 2111;
    TXTATTRIB_AGATE = 2115;

    TXTATTRIB_TRADE_BOARD = 2201;
    TXTATTRIB_FRIEND_BOARD = 2202;
    TXTATTRIB_TEAM_BOARD = 2203;
    TXTATTRIB_SYN_BOARD = 2204;
    TXTATTRIB_OTHER_BOARD = 2205;

    TXTATTRIB_BROADCAST = 2500;
}
```

#### Text Style

☑️ Assumed (Observed) - Chimera

```proto
enum TextStyle {

    TXTSTYLE_NORMAL = 0;
    TXTSTYLE_SCROLL = 0x01;
    TXTSTYLE_FLASH = 0x02;
    TXTSTYLE_BLAST = 0x08;
}
```

## Patch 5808

#### Message Definition

❓ Unverified - Imported from the legacy wiki

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 56 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1004 |
| 4  | UInt32 | [System Time](/network/timestamp.md) | Milliseconds of system uptime | 1579535985 |
| 8  | Int32 | Text Color | [ARGB32](https://en.wikipedia.org/wiki/RGBA_color_model) color of the text | 00FF0000 |
| 12 | UInt16 | [Text Attribute](#text-attribute-1) | Defines where the text appears | 2000 |
| 14 | Uint16 | [Text Style](#text-style-1) | Defines how the text appears | 0 |
| 16 | UInt32 | [Local Time](/network/timestamp.md) | Hours and minutes | 1241 |
| 20 | UInt32 | Hearer [View](/algorithms/calculations/roleview.md) | Character view mesh for the hearer | 501002 |
| 24 | UInt32 | Speaker [View](/algorithms/calculations/roleview.md) | Character view mesh for the speaker | 501002 |
| 28 | [NetStringPacker](/network/stringpacker.md) | Strings | Group of length prefixed strings | |

#### NetStringPacker Fields

| Name | Description | Example |
|:-------|:--------|:--------|
| Speaker | Author of the message | SYSTEM |
| Header | Recipient of the message | ALLUSERS |
| Emotion | A prefix to the message | |
| Words | The body of the message | Testing |
| Unknown | Not referenced in the client assembly | |
| Unknown | Not referenced in the client assembly | |

#### Text Attribute

❓ Unverified - Imported from the legacy wiki

```proto
enum TextAttribute {

    TXTATTRIB_UNSPECIFIED = 0;
    TXTATTRIB_NORMAL = 2000;
    TXTATTRIB_WHISPER = 2001;
    TXTATTRIB_ACTION = 2002;
    TXTATTRIB_TEAM = 2003;
    TXTATTRIB_SYNDICATE = 2004;
    TXTATTRIB_FAMILY = 2006;
    TXTATTRIB_SYSTEM = 2007;
    TXTATTRIB_YELL = 2008;
    TXTATTRIB_FRIEND = 2009;
    TXTATTRIB_GM = 2011;
    TXTATTRIB_NOTIFICATION = 2012;
    TXTATTRIB_GHOST = 2013;
    TXTATTRIB_SERVICE = 2014;
    TXTATTRIB_TIP = 2015;
    TXTATTRIB_WORLD = 2021,
    TXTATTRIB_QUALIFIER = 2022,
    TXTATTRIB_STUDY = 2024,

    TXTATTRIB_REGISTER = 2100;
    TXTATTRIB_LOGIN = 2101;
    TXTATTRIB_SHOP = 2102;
    TXTATTRIB_PET = 2103;
    TXTATTRIB_VENDOR = 2104;
    TXTATTRIB_WEBPAGE = 2105;
    TXTATTRIB_SYNWAR_FIRST = 2108;
    TXTATTRIB_SYNWAR_NEXT = 2109;
    TXTATTRIB_LEAVE_WORD = 2110;
    TXTATTRIB_SYNANNOUNCE = 2111;
    TXTATTRIB_AGATE = 2115;

    TXTATTRIB_TRADE_BOARD = 2201;
    TXTATTRIB_FRIEND_BOARD = 2202;
    TXTATTRIB_TEAM_BOARD = 2203;
    TXTATTRIB_SYN_BOARD = 2204;
    TXTATTRIB_OTHER_BOARD = 2205;

    TXTATTRIB_BROADCAST = 2500;
}
```

#### Text Style

❓ Unverified - Imported from the legacy wiki

```proto
enum TextStyle {

    TXTSTYLE_NORMAL = 0;
    TXTSTYLE_SCROLL = 0x01;
    TXTSTYLE_FLASH = 0x02;
    TXTSTYLE_BLAST = 0x08;
}
```
