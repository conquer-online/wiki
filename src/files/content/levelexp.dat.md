# LevelExp.dat

This file was used in Conquer 1.0 and some early Conquer 2.0 patches (superseded by [LevExp.dat](./levexp.dat.md))

It maps each level to the experience points required to reach the next level.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

☑️ Assumed (Soul)

### File Structure

The file is a flat array of `UInt32` values, one per level. Levels start at 1, where `i` is the zero-based array index:

| Offset  | Type   | Description              |
|:--------|:-------|:-------------------------|
| `i * 4` | UInt32 | EXP to reach level `i+1` |

### Encryption

Each `UInt32` in the file is XOR-encrypted using a hardcoded 27-byte Chinese string: `★就这样被你蒸熟★`.

In bytes, this UTF-8 string is: `E2 98 85 E5 B0 B1 E8 BF 99 E6 A0 B7 E8 A2 AB E4 BD A0 E8 92 B8 E7 86 9F E2 98 85` which is used as the XOR key (each byte treated as a signed char).

### Example Entries

| Level | EXP Required |
|:------|:-------------|
| 1     | 59           |
| 2     | 195          |
| 3     | 203          |
| 4     | 320          |
| 5     | 573          |
| ...   | ...          |

### Parsing Script

The following Python script decodes `LevelExp.dat` and prints each level alongside its EXP requirement.

Pass the filepath as the first argument. Example: `python3 levelexp_decode.py LevelExp.dat`

```python
import struct, sys, math

KEY = bytes.fromhex("E29885E5B0B1E8BF99E6A0B7E8A2ABE4BDA0E892B8E7869FE29885")

with open(sys.argv[1], "rb") as f:
    data = f.read()

    count = math.floor(len(data) / 4) # Find number of levels based on file size
    values = struct.unpack(f"<{count}I", data)

    for level in range(1, count + 1):
        key_byte = KEY[(level - 1) % len(KEY)]
        mask = (key_byte | 0xFFFFFF00) if key_byte > 0x7F else key_byte # Signed Byte
        exp = (values[level - 1] ^ mask) & 0xFFFFFFFF
        print(f"Level {level}: {exp} EXP")
```
