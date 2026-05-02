# Action.dat

This file was used in Conquer 1.0 (patches 4267 & below). Although this file is distributed with Conquer 2.0, the code that consumes it is dead code in the client binary, so it is not used in Conquer 2.0.

It maps some [ActionType](../../constants/actions.md) to specify the length of each animation frame in milliseconds. 

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

☑️ Assumed (Soul)

### File Header

| Offset | Type   | Description                   |
|:-------|:-------|:------------------------------|
| 0      | UInt32 | Number of records in the file |

### Record Structure

| Offset | Type   | Description         |
|:-------|:-------|:--------------------|
| 0      | UInt32 | Checksum 1          |
| 4      | UInt32 | Action Index        |
| 8      | UInt32 | Checksum 2          |
| 12     | UInt32 | Frame Interval (ms) |
| 16     | UInt32 | Checksum 3          |

Each record is 20 bytes. There are three checksum fields computed using the value of the Action Index and its position `i`, starting from zero.

```
Checksum1 = (ActionIndex * 2) + (FrameInterval + i)
Checksum2 = (i * Checksum1) + (ActionIndex * FrameInterval) - i
Checksum3 = (Checksum1 * ActionIndex) + (Checksum2 * 7) + (FrameInterval * i)
```

The client errors on checksum mismatch. The checksums are likely anti-tamper protection against manipulating animation speeds.

### Action Index Structure

`ActionIndex` is made up of three components as a single integer:

```
ActionIndex = (LookFace * 1000000) + (WeaponType * 1000) + ActionType
```

When any component is set to `999`, the code has specific logic as match-any, effectively a wildcard.

As an example: `999999110`

* Digits 7-9 = `999` = Match any LookType (Male / Female / Transform)
* Digits 4-6 = `999` = Match any WeaponType (Bow / Club / Dual-Wield / Shield etc.)
* Digits 1-3 = `110` = Matches [ActionType](../../constants/actions.md) `ACTION_WALKL` (Walk Left)

For `999999110`, the frame interval is `25`, so each frame in the animation has a 25ms delay. 

### Example Entries

| Action Index | Frame Interval (ms) |
|:-------------|:--------------------|
| 999999100    | 66                  |
| 999999101    | 66                  |
| 999999110    | 25                  |
| 999999120    | 25                  |
| 999999130    | 33                  |
| ...          | ...                 |

### Parsing Script

The following is a simple python script which reads and parses `Action.dat`.

Pass the filepath as the first arg & it will print each action index alongside its time interval. Checksums won't be printed. Example: `python3 action_decode.py Action.dat`

```python
import struct, sys

with open(sys.argv[1], "rb") as f:
    count, = struct.unpack("<I", f.read(4))  # Little-Endian uint32 - Header (Record Count)
    for i in range(count):
        # checksum1, action_index, checksum2, frame_interval, checksum3
        _, action_index, _, frame_interval, _ = struct.unpack("<IIIII", f.read(20))
        print(f"{action_index}: {frame_interval}ms")
```
