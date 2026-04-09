# AutoAllot.dat

Although this file was distributed with the client, it is **never referenced or used** in any known version (at least 4217 to 6090). It was most likely moved to the server side database (table: `cq_point_allot`) and the file was never removed from the client. It maps the distribution of Strength (Force), Agility (Speed), Vitality (Health), and Spirit (Soul) attribute points for each level before first Rebirth and up to level 120.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

☑️ Assumed (Soul)

### File Header

| Offset | Type   | Description     |
|:-------|:-------|:----------------|
| 0      | UInt32 | ProfessionCount |
| 4      | UInt32 | LevelCount      |

#### Profession Index

After the header is an array of [ProfessionType](./ProfessionalName.ini.md). `i` is the array index, starting from zero:

| Offset        | Type   | Description                                 |
|:--------------|:-------|:--------------------------------------------|
| `8 + (i * 4)` | UInt32 | [ProfessionType](./ProfessionalName.ini.md) |

#### Data Records

Then an array of `ProfessionCount * LevelCount` records, ordered by ProfessionType then level:

| Offset (per record) | Type   | Description |
|:--------------------|:-------|:------------|
| 0                   | UInt32 | Strength    |
| 4                   | UInt32 | Agility     |
| 8                   | UInt32 | Vitality    |
| 12                  | UInt32 | Spirit      |

Level is not stored, it is implicit from the position in the array. 

### Example Entries

| ProfessionType | Level | Strength | Agility | Vitality | Spirit |
|:---------------|:------|:---------|:--------|:---------|:-------|
| 1              | 1     | 5        | 2       | 3        | 0      |
| 1              | 2     | 7        | 2       | 4        | 0      |
| 1              | 3     | 8        | 3       | 5        | 0      |
| 1              | 4     | 10       | 4       | 5        | 0      |
| 1              | 5     | 11       | 5       | 6        | 0      |
| ...            | ...   | ...      | ...     | ...      | ...    |

### Parsing Script

The following Python script decodes `AutoAllot.dat` and prints the allocation table for every profession and level.

Pass the filepath as the first argument. Example: `python3 autoallot_decode.py AutoAllot.dat`

```python
import struct, sys

with open(sys.argv[1], "rb") as f:
    prof_count, level_count = struct.unpack("<II", f.read(8))
    index = struct.unpack(f"<{prof_count}I", f.read(prof_count * 4))

    for i in range(prof_count):
        prof_type = index[i]
        for level in range(1, level_count + 1):
            strength, agility, vitality, spirit = struct.unpack("<IIII", f.read(16))
            print(f"ProfessionType={prof_type}, Level {level}: "
                  f"Strength={strength} Agility={agility} Vitality={vitality} Spirit={spirit}")
```
