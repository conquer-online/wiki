# GameMap.dat

This file is loaded when the client starts. It maps the Map IDs to either the [DMap](../../files/formats/dmap.md) or, in later clients, its compressed archive equivalent (`.7z` files).


## Table of Contents

* [Patch 5517](#patch-5517)

## Patch 5517

### File Header

| Offset | Size | Type   | Description                   |
|:-------|:-----|:-------|:------------------------------|
| 0      | 4    | UInt32 | Number of records in the file |

### Record Structure

| Offset     | Size     | Type   | Description                   | Example             |
|:-----------|:---------|:-------|:------------------------------|:--------------------|
| 0          | 4        | UInt32 | Map ID                        | `1000`              |
| 4          | 4        | UInt32 | Length of the filepath        | `17`                |
| 8          | [Length] | String | Map path (Ascii Unterminated) | `map/map/desert.7z` |
| 8 + Length | 4        | UInt32 | Unknown - Always 256          | `256`               |

### Example Entries

| Map ID | Archive Path           |
|:-------|:-----------------------|
| 1000   | `map/map/desert.7z`    |
| 1001   | `map/map/d_antre01.7z` |
| 1002   | `map/map/newplain.7z`  |
| 1003   | `map/map/mine01.7z`    |
| ...    | ...                    |

### Parsing Script

The following is a simple python script which reads and parses the `GameMap.dat`. Pass the filepath as the first arg & it will output each map ID alongside its path. Example: `python3 gamemap_decode.py GameMap.dat`

```python
import struct, sys

with open(sys.argv[1], "rb") as f:
    count, = struct.unpack("<I", f.read(4)) # Little-Endian uint32 - Header (Record Count)
    for idx in range(count):
        map_id, name_len = struct.unpack("<II", f.read(8)) # Read ID & Length of Map Name
        name = f.read(name_len).decode("ascii") # Read the map name
        f.read(4) # Unknown field, always 256
        print(f"{map_id}: {name}")
```
