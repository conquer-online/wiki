# MsgMapInfo

This small game server message is sent to instruct the client on which [data map](../../files/formats/dmap.md) document to load from and what map type flags apply to it. This allows the game server to create unique duplicates of a map that reference one single data map.

Rather than referencing the file path to the DMap in the message, an identifier is used as a key for looking up the path in [GameMap.dat](../../files/content/gamemap.dat.md).

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

✅ Verified (Client)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 16 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1110 |
| 4  | UInt32 | [Map ID](../identifiers.md) | Map identifier | 1002 |
| 8  | UInt32 | [Doc ID](../../files/content/gamemap.dat.md) | DMap identifier | 1002 |
| 12 | UInt32 | [Type](#map-type-flags) | Map type flags | 0 |

#### Map Type Flags

☑️ Assumed (Soul)

```proto
enum MapTypeFlags {
    MAPTYPE_NORMAL = 0x0000,
    MAPTYPE_PKFIELD = 0x0001,
    MAPTYPE_CHGMAP_DISABLE = 0x0002,
    MAPTYPE_RECORD_DISABLE = 0x0004,
    MAPTYPE_PK_DISABLE = 0x0008,
    MAPTYPE_BOOTH_ENABLE = 0x0010,
    MAPTYPE_TEAM_DISABLE = 0x0020,
    MAPTYPE_TELEPORT_DISABLE = 0x0040,
    MAPTYPE_SYN_MAP = 0x0080,
    MAPTYPE_PRISON_MAP = 0x0100,
    MAPTYPE_FLY_DISABLE = 0x00200,
    MAPTYPE_FAMILY = 0x00400,
    MAPTYPE_MINEFIELD = 0x0800,
    MAPTYPE_PKGAME = 0x1000,
}
```
