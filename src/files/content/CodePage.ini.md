# CodePage.ini

Sets the Windows code page (character set) used by `graphic.dll` to decode multibyte character strings for font rendering. Read by client immediately after [font.ini](./font.ini.md).

This file does not exist by default with the English distribution, but can be created.

## Table of Contents

* [Patch 5517](#patch-5517)

## Patch 5517

✅ Verified (Client)

Located at `ini/CodePage.ini`.

### Example Entries

```
936
```

The first line is read as an integer and used by C3_CORE_DLL font functions to convert multibyte sequences to Unicode before FreeType rendering.


### Common code page values

| Value  | Encoding     | Region              |
|:-------|:-------------|:--------------------|
| `936`  | GBK          | Simplified Chinese  |
| `950`  | Big5         | Traditional Chinese |
| `932`  | Shift-JIS    | Japanese            |
| `949`  | EUC-KR       | Korean              |
| `1256` | Windows-1256 | Arabic              |

If this file is absent, multibyte characters will not decode correctly, preventing non-ASCII text from rendering.
