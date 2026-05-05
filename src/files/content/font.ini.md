# font.ini

Tells `graphic.dll` which font file to load via FreeType and at what size. Read by the client at startup.

Used as a fallback if [FontSetting.ini](./FontSetting.ini.md) is not present or its values are not set or invalid.

## Table of Contents

* [Patch 5517](#patch-5517)

## Patch 5517

✅ Verified (Client)

Located at `ini/font.ini`.

The file contains a single line in the format:

```
<fontname> <size>
```

| Part       | Description                                                                                      |
|:-----------|:-------------------------------------------------------------------------------------------------|
| `fontname` | Font filename in the client root, or an installed Windows font name.                             |
| `size`     | Default font size (int). Falls back to `12` if `0` or missing.                                   |

### Examples

Load `simsun.ttf` from the client root folder at size 14:

```
simsun.ttf 14
```
