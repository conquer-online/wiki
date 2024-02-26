# MsgWalk

This message is sent from the game client when the player moves on the ground in a direction. The server responds by validating the movement and then sending the movement to all observers within the player's screen. If the observer receives a MsgWalk message for a player that doesn't exist on their screen, then that'll trigger a [MsgAction](msgaction.md) request for that player using the QueryPlayer action.

> ⚠️ __WARNING__
>
>  Although the client checks for invalid coordinates, a modified client can walk on invalid tiles or across occupied spaces (such as the guild gate). Be sure to validate the coordinates of movements on the server side.

## Table of Contents

* [Patch 4267](#patch-4267)
* [Patch 5165](#patch-5165)
* [Patch 5517](#patch-5517)
* [Patch 6132](#patch-6132)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul) 

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 10 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1005 |
| 4  | UInt32 | [Hero ID](/network/identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | Byte | [Direction](/algorithms/calculations/direction.md) | Movement direction | 0 |
| 9  | Bool | Run | True if the player is running | 1 |

## Patch 5165

#### Message Definition

☑️ Assumed (Observed)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 16 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1005 |
| 4  | UInt32 | [Direction](/algorithms/calculations/direction.md) | Movement direction | 0 |
| 8  | UInt32 | [Hero ID](/network/identifiers.md) | Unique identifier for the character | 1000000 |
| 12 | UInt32 | [Movement Mode](#movement-modes) | Type of ground movement | 1 |

#### Movement Modes

☑️ Assumed (Observed)

```proto
enum MovementModes {

    MOVEMENT_MODE_WALK = 0;
    MOVEMENT_MODE_RUN = 1;
    MOVEMENT_MODE_MOUNTED = 9;
}
```

## Patch 5517

#### Message Definition

☑️ Assumed (Observed)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 24 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 10005 |
| 4  | UInt32 | [Direction](/algorithms/calculations/direction.md) | Movement direction | 0 |
| 8  | UInt32 | [Hero ID](/network/identifiers.md) | Unique identifier for the character | 1000000 |
| 12 | UInt32 | [Movement Mode](#movement-modes-1) | Type of ground movement | 1 |
| 16 | UInt32 | [System Time](/network/timestamps.md) | Milliseconds of system uptime | 10000 |
| 20 | UInt32 | [Map ID](/files/content/gamemap.dat.md) | Map identifier | 1002 |

#### Movement Modes

☑️ Assumed (Observed)

```proto
enum MovementModes {

    MOVEMENT_MODE_WALK = 0;
    MOVEMENT_MODE_RUN = 1;
    MOVEMENT_MODE_MOUNTED = 9;
}
```

## Patch 6132

#### Message Definition

❓ Unverified - Imported from the legacy wiki

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 24 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 10005 |
| 4  | Bytes | [Protobuf](#protobuf-fields) | Serialized protobuf fields | |

#### Protobuf Fields

❓ Unverified - Imported from the legacy wiki

| Type | Name | ID | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| UInt32 | [direction](/algorithms/calculations/direction.md) | 1 | Movement direction | 0 |
| UInt32 | [hero_id](/network/identifiers.md) | 2 | Unique identifier for the character | 1000000 |
| UInt32 | [movement_mode](#movement-modes-1) | 3 | Type of ground movement | 1 |
| UInt32 | [system_time](/network/timestamps.md) | 4 | Milliseconds of system uptime | 10000 |
| UInt32 | [map_id](/files/content/gamemap.dat.md) | 5 | Map identifier | 1002 |

#### Movement Modes

❓ Unverified - Imported from the legacy wiki

```proto
enum MovementModes {

    MOVEMENT_MODE_WALK = 0;
    MOVEMENT_MODE_RUN = 1;
    MOVEMENT_MODE_MOUNTED = 9;
}
```
