# Item ID

Item IDs are structured integers that encode information such as the item's category, type, level and quality directly in the number. 

[ItemType.dat](../files/content/itemtype.dat.md) is the file the client uses to find the details about an item id.

## Table of Contents

* [Patch 5517](#patch-5517)

## Patch 5517

### Fields

Three fields can always be extracted from any Item ID:

| Field        | Formula                   | Description                                        |
|:-------------|:--------------------------|:---------------------------------------------------|
| Item Quality | `id % 10`                 | [Quality grade (0-9)](#item-quality-grade)         |
| Item Level   | `floor(id / 10) % 100`    | Level of the item (name / stats)                   |
| Category     | `floor(id / 10000) % 100` | Two-digit item category (equipment & weapons only) |

### Item Quality Grade

For equipment and gems, the last digit of the item ID is the quality, where a higher quality digit means increased stats. The exception is quality digit `0` (Fixed) which applies to low-level equipment (`level < 52`) & stats can exceed Super quality but the item cannot be upgraded.

For all other item types, the last digit sometimes acts as a variant identifier or isn't used.

#### Equipment Quality

| Digit | Name                                              |
|:------|:--------------------------------------------------|
| 0     | Fixed                                             |
| 1     | Starting Gear for New Players (Normal)            |
| 2     | Unused 🔵                                         |
| 3     | Normal _(Base Stats)_                             |
| 4     | Normal _(Typically Base + Slight Stat Increase)_  |
| 5     | Normal _(Typically Base + Further Stat Increase)_ |
| 6     | Refined                                           |
| 7     | Unique                                            |
| 8     | Elite                                             |
| 9     | Super                                             |

🔵 There is only one item with quality digit `2`: `131052` (Lv57 Warrior ChainedArmor). There is no explanation for this, it is suspected to be a developer mistake.

#### Gems Quality

| Digit | Name    |
|:------|:--------|
| 1     | Normal  |
| 2     | Refined |
| 3     | Super   |

### Overall Item ID Ranges

| ID Range          | Description                                                                        |
|:------------------|:-----------------------------------------------------------------------------------|
| `100000-199999`   | [Equipment](#equipment-ranges) (Head, Necklace, Ring, Bracelets, Armor, Garments)  |
| `200000-209999`   | Mount Armor, Fan & Tower                                                           |
| `300000-309999`   | Mounts (Only Single Entry: `Steed`)                                                |
| `400000-499999`   | [Single-hand weapons](#single-hand-4xxxxx--6xxxxx) _(excluding Katanas & Beads)_   |
| `500000-599999`   | [Two-hand weapons](#two-hand-5xxxxx)                                               |
| `600000-699999`   | [Single-hand Weapons: Katanas (Ninja) & Beads (Monk)](#single-hand-4xxxxx--6xxxxx) |
| `700000-799999`   | Gems, Item Packs, Quest Items, Furniture, Refinery Items                           |
| `800000-899999`   | Dragon & Martial Souls                                                             |
| `900000-999999`   | Shields                                                                            |
| `1000000-1099999` | Consumables, arrows, ores, Dragonball/Meteor & Silver/Gold                         |
| `2000000-2999999` | Gourd & Talismans                                                                  |

There is a single item that falls outside these ranges: `ID: 50000 Name: Speed Arrow`, but this item has an invalid icon & the real Speed Arrow ID is: `1050002`. This is an invalid (perhaps legacy) record. 


#### Equipment Ranges

| ID Range      | Equipment type   |
|:--------------|:-----------------|
| 110000-119999 | Head gear        |
| 120000-129999 | Necklaces        |
| 130000-139999 | Body armor       |
| 140000-149999 | Head gear        |
| 150000-159999 | Rings, bracelets |
| 160000-169999 | Boots            |
| 180000-189999 | Garments         |
| 190000-199999 | Garments         |

#### Weapon Ranges

##### Single-hand (`4xxxxx` & `6xxxxx`):

| ID Range      | Weapon type  |
|:--------------|:-------------|
| 410000-419999 | Blade        |
| 420000-429999 | Sword        |
| 430000-439999 | Hook         |
| 440000-449999 | Whip         |
| 450000-459999 | Axe          |
| 460000-469999 | Hammer       |
| 480000-489999 | Club         |
| 490000-499999 | Dagger       |
| 600000-609999 | Katana       |
| 610000-619999 | Prayer Beads |

##### Two-hand (`5xxxxx`):

| ID Range      | Weapon type   |
|:--------------|:--------------|
| 500000-509999 | Bow           |
| 510000-519999 | Glaive        |
| 530000-539999 | Poleaxe       |
| 540000-549999 | Long Hammer   |
| 560000-560999 | Spear         |
| 561000-561999 | Wand          |
| 562000-562001 | Pickaxe & Hoe |
| 580000-589999 | Halberd       |
