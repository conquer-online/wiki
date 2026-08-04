# MsgRankMemberShow

Not present in earlier client versions and not covered by this wiki before. It is sent by the client right after a [MsgRank](msgrank.md) `PROFESSION_TOPS` request, and the reply drives the 3D model shown in the "Best in the World" panel of `CDlgProfessionalRank`. Without a reply the panel keeps the name and score from `MsgRank` but the model stays empty.

The message body is a protobuf, and the client is built with `LITE_RUNTIME`, so there are no field descriptors in the binary to recover names from. The field numbers below were read directly out of `CMemberShowInfoPB::SerializeWithCachedSizes`; the names are inferred from how the client consumes each field, not from the binary itself.

## Table of Contents

* [Patch 6609](#patch-6609)

## Patch 6609

✅ **Verified (Client)**: Confirmed by reverse engineering the 6609 client binary.

#### Message Definition

| Pos | Type  | Name                          | Description                 | Example |
|:----|:------|:-------------------------------|:-----------------------------|:--------|
| 0   | UInt16 | [MsgSize](index.md#message-header) | Size of the message      | -       |
| 2   | UInt16 | [MsgType](index.md#message-header) | Type of message           | 3257    |
| 4   | Bytes  | [Protobuf](#protobuf-fields)  | Serialized protobuf fields  | -       |

#### Protobuf Fields

| Type   | Name          | ID | Description                                                                 | Example |
|:-------|:--------------|:---|:------------------------------------------------------------------------------|:--------|
| UInt32 | status        | 1  | `0` on success. `1` makes the client show "Failed to view. The target is offline." | 0 |
| Bytes  | [member](#member-fields) | 2  | Repeated `CMemberShowInfoPB`. Only the last entry with `kind == 1` is drawn | -       |

#### Member Fields

`CMemberShowInfoPB`, embedded in field `2` above.

| Type   | Name                | ID | Description                                                        | Example  |
|:-------|:---------------------|:---|:----------------------------------------------------------------------|:---------|
| UInt32 | kind                 | 1  | The client only draws entries where this is `1`                        | 1        |
| UInt32 | request              | 2  | Request-only selector, not read back from the reply                    | 1        |
| UInt32 | [hero_id](../identifiers.md) | 3  | Must be non-zero or the entry is treated as empty              | 1000001  |
| String | -                    | 4  | Unused by this panel                                                    | -        |
| String | name                 | 5  | Hero name                                                                | Carniato |
| UInt32 | [look_face](../../constants/lookface.md) | 6 | Hero mesh                                              | 2011     |
| UInt32 | [hairstyle](../../constants/hairstyles.md) | 7 | Hero hairstyle                                       | 535      |
| UInt32 | headgear             | 8  | Item at equipment position 1                                             | 118109   |
| UInt32 | armor                | 9  | Item at equipment position 3, or the garment if one is worn               | 133009   |
| UInt32 | left_hand            | 10 | Item at equipment position 5                                            | 900309   |
| UInt32 | left_hand_addition   | 11 | Item at equipment position 16                                            | 201009   |
| UInt32 | right_hand           | 12 | Item at equipment position 4                                            | 410309   |
| UInt32 | right_hand_addition  | 13 | Item at equipment position 15                                            | 200009   |
| UInt32 | mount_armor          | 14 | Item at equipment position 17                                            | 200000   |
| UInt32 | mount_armor_addition | 15 | Not confirmed                                                            | 0        |
| UInt32 | mount                | 16 | Item at equipment position 12                                            | 300000   |
| UInt32 | mount_addition       | 17 | Not confirmed                                                            | 0        |
| UInt32 | garment_effect       | 18 | Not confirmed                                                            | 0        |
| UInt32 | aura                 | 19 | Not confirmed                                                            | 0        |

The request the client sends has a single member entry with `kind = 1` and `request` set to whichever rank type box was clicked; the reply does not need to echo `request` back.
