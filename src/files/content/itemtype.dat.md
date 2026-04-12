# ItemType.dat

This file is loaded when the client starts. It defines every item in the game such as equipment, weapons, consumables, mounts, soul/purification, garments, crafting materials, and more.

Records in `itemtype.dat` are the default values for the item, [MsgItemInfo](../../network/messages/msgiteminfo.md) can be used to supply some of the dynamic values (such as the socketed gems or expiration time)

See [Item ID](../../constants/itemid.md) for the full breakdown of how Item IDs encodes information such category, weapon type, item level & quality for equipment.

## Table of Contents

* [Patch 5517](#patch-5517)

## Patch 5517

In Patch 5517, this file is encrypted with [**TQ File Cipher**](../../security/tqfile.md) with seed: `9527` (`0x2537`).

### File Format

After decryption, the file is plain-text with an item record-per-line. Each field is separated by `@@` and ends with a trailing `@@\r\n`.

`~` is used as space characters and backticks (`` ` ``) used as apostrophe in fields such as item name and description.

### Record Structure

| Field | Name                 | Type   | Description                                                                                                                                   |
|:------|:---------------------|:-------|:----------------------------------------------------------------------------------------------------------------------------------------------|
| 1     | `id`                 | uint32 | [Item ID](../../constants/itemid.md)                                                                                                          |
| 2     | `name`               | string | Item Name                                                                                                                                     |
| 3     | `req_profession`     | uint8  | Required [Hero Profession](../../constants/heroprofession.md)                                                                                 |
| 4     | `req_weaponskill`    | uint8  | Required Weapon Proficiency level                                                                                                             |
| 5     | `req_level`          | uint8  | Minimum character level required to equip or use                                                                                              |
| 6     | `req_sex`            | uint8  | Hero restriction (0=any, 1=Male , 2=Female)                                                                                                   |
| 7     | `req_force`          | uint16 | Required Strength attribute amount                                                                                                            |
| 8     | `req_speed`          | uint16 | Required Agility attribute amount                                                                                                             |
| 9     | `req_health`         | uint16 | Required Vitality attribute amount                                                                                                            |
| 10    | `req_soul`           | uint16 | Required Spirit attribute amount                                                                                                              |
| 11    | `monopoly`           | uint8  | Bitmask trade, warehouse, bound, lock & drop restrictions                                                                                     |
| 12    | `weight`             | uint16 | Used on a few event item tooltips                                                                                                             |
| 13    | `price`              | int32  | NPC buy price in silver                                                                                                                       |
| 14    | `id_action`          | int32  | Script or action ID to trigger on use or equip (0 = none)                                                                                     |
| 15    | `attack_max`         | uint16 | Maximum physical attack                                                                                                                       |
| 16    | `attack_min`         | uint16 | Minimum physical attack                                                                                                                       |
| 17    | `defense`            | uint16 | Physical defense bonus                                                                                                                        |
| 18    | `agility`            | uint16 | Agility bonus                                                                                                                                 |
| 19    | `dodge`              | uint16 | Dodge bonus                                                                                                                                   |
| 20    | `life`               | uint16 | HP bonus                                                                                                                                      |
| 21    | `mana`               | uint16 | MP bonus                                                                                                                                      |
| 22    | `durability`         | uint16 | Default durability                                                                                                                            |
| 23    | `durability_limit`   | uint16 | Maximum durability                                                                                                                            |
| 24    | `identified`         | uint8  | Unused                                                                                                                                        |
| 25    | `gem1`               | uint8  | Socket 1 Gem [Item ID](../../constants/itemid.md) (0 = empty socket)                                                                          |
| 26    | `gem2`               | uint8  | Socket 2 Gem [Item ID](../../constants/itemid.md) (0 = empty socket)                                                                          |
| 27    | `magic1`             | int32  | Unused, set via [MsgItemInfo](../../network/messages/msgiteminfo.md)                                                                          |
| 28    | `magic2`             | uint8  | Unused, set via [MsgItemInfo](../../network/messages/msgiteminfo.md)                                                                          |
| 29    | `n_amount`           | uint8  | +N item value & +N item stones                                                                                                                |
| 30    | `data`               | int32  | Unused, set via [MsgItemInfo](../../network/messages/msgiteminfo.md) for additional attributes (socket progress, container amount)            |
| 31    | `magic_atk`          | uint16 | Magic attack bonus                                                                                                                            |
| 32    | `magic_def`          | uint16 | Magic defense bonus                                                                                                                           |
| 33    | `atk_range`          | uint16 | Attack range                                                                                                                                  |
| 34    | `atk_speed`          | uint16 | Attack speed                                                                                                                                  |
| 35    | `fray_mode`          | uint8  | Unknown `0` on all normal equipment. `2` on garments & mount armor. _(Suspected: Different durability algorithm for garments)_                |
| 36    | `repair_mode`        | uint8  | Unknown `0` on normal equipment. `2` on garments & mount armor. `3` on gourds. _(Suspected: Different repair mechanic for garments / gourds)_ |
| 37    | `type_mask`          | uint8  | Is set to `1` on Cosmetic Equipment (Garments / Mounts) appears client uses it in Character Pose Actions (Unknown purpose)                    |
| 38    | `emoney_price`       | int32  | Conquer Points (CP) shop price. `0` = not sold for CP                                                                                         |
| 39    | `emoney_bound_price` | int32  | Bound Conquer Points (CP) Shop Price. `0` = not sold for Bound CP                                                                             |
| 40    | `expiry_time`        | int32  | Item duration in minutes. Used on some mounts, cosmetics & quest items                                                                        |
| 41    | `soul_atk_1`         | int32  | Soul - Critical Strike percentage bonus `(value / 100)%`                                                                                                 |
| 42    | `soul_atk_2`         | int32  | Soul - Skill Critical Strike percentage bonus`(value / 100)%`                                                                                            |
| 43    | `soul_def_1`         | int32  | Soul - Immunity percentage bonus `(value / 100)%`                                                                                                        |
| 44    | `soul_atk_3`         | int32  | Soul - Penetration percentage bonus `(value / 100)%`                                                                                                     |
| 45    | `soul_def_2`         | int32  | Soul - Block percentage bonus `(value / 100)%`                                                                                                           |
| 46    | `soul_atk_4`         | int32  | Soul - Breakthrough percentage bonus `(value / 10)%`                                                                                                     |
| 47    | `soul_def_3`         | int32  | Soul - Counteraction percentage bonus `(value / 10)%`                                                                                                    |
| 48    | `max_stack_size`     | int32  | Maximum amount the same item can be stacked in same item slot                                                                                 |
| 49    | `elem_res_metal`     | int32  | Metal element resistance bonus (unused)                                                                                                       |
| 50    | `elem_res_wood`      | int32  | Wood element resistance bonus                                                                                                                 |
| 51    | `elem_res_water`     | int32  | Water element resistance bonus                                                                                                                |
| 52    | `elem_res_fire`      | int32  | Fire element resistance bonus                                                                                                                 |
| 53    | `elem_res_earth`     | int32  | Earth element resistance bonus                                                                                                                |
| 54    | `item_type`          | string | Tooltip description of the item type                                                                                                          |
| 55    | `description`        | string | Tooltip long description about the item                                                                                                       |
| 56    | `quality_color`      | int32  | For non-equipment, the item color. Quality value same as [Equipment Quality](../../constants/itemid.md)                                       |
| 57    | `dragonsoul_phase`   | uint16 | Dragonsoul phase number (1-6)                                                                                                                 |
| 58    | `dragonsoul_req`     | int32  | Dragonsoul requirement to reach next phase                                                                                                    |
| 59    | `crop_quality`       | int32  | Only used by item `Riding Crop` quality (1=Unique, 2=Elite, 3=Super)                                                                          |

### Parsing Script (To CSV)

You must first decrypt `itemtype.dat` using [**TQ File Cipher**](../../security/tqfile.md) with seed: `9527` (`0x2537`). Then you can use this python script to parse the file and output it as a `CSV` file. 

Pass the decrypted `itemtype.dat` path as the first arg & it will output a csv called `itemtype.csv`. This script has **no error handling, checks or dependencies** as it is intentionally kept minimal for readability.

Example: `python3 itemtype_decode.py itemtype_decrypted.dat`

```python
import csv
import sys

# This script has only been tested on client 5517 itemtype.dat. Other patches may have a different amount of fields so this script will not work

FIELD_SEP = "@@"

FIELDS = [
    "id", "name", "req_profession", "req_weaponskill", "req_level", "req_sex",
    "req_force", "req_speed", "req_health", "req_soul", "monopoly", "weight",
    "price", "id_action", "attack_max", "attack_min", "defense", "agility",
    "dodge", "life", "mana", "durability", "durability_limit", "identified",
    "gem1", "gem2", "magic1", "magic2", "n_amount", "data", "magic_atk",
    "magic_def", "atk_range", "atk_speed", "fray_mode", "repair_mode", "type_mask",
    "emoney_price", "emoney_bound_price", "expiry_time", "soul_atk_1", "soul_atk_2",
    "soul_def_1", "soul_atk_3", "soul_def_2", "soul_atk_4", "soul_def_3",
    "max_stack_size", "elem_res_metal", "elem_res_wood", "elem_res_water",
    "elem_res_fire", "elem_res_earth", "item_type", "description",
    "quality_color", "dragonsoul_phase", "dragonsoul_req", "crop_quality",
]

input_path  = sys.argv[1]
output_path = sys.argv[2] if len(sys.argv) > 2 else "itemtype.csv"

# Some items have chinese characters (gbk encoding) & mark unknown characters with '?'
with open(input_path, "r", encoding="gbk", errors="replace") as f_in, \
     open(output_path, "w", newline="", encoding="utf-8") as f_out:

    writer = csv.writer(f_out)
    writer.writerow(FIELDS)
    skipped = 0
    rows_extracted = 0

    for line in f_in:
        line = line.strip()
        if not line:
            continue
        parts = line.split(FIELD_SEP)
        if parts and parts[-1] == "":
            parts = parts[:-1]
        if len(parts) != len(FIELDS):
            skipped += 1
            continue
        writer.writerow(parts)
        rows_extracted += 1

    if skipped > 0:
        print(f"Warning: {skipped} rows were skipped as they had an incorrect amount of fields.")

print(f"Completed {rows_extracted} extracted from {input_path} to {output_path}")
    
```
