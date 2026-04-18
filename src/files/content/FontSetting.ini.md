# FontSetting.ini

Configures the fonts used for in-game text rendering. Read once at startup by the client. If the file or font does not exist, it falls back to the value in [font.ini](./font.ini.md).

This file does not exist by default with the English distribution, but can be created.

## Table of Contents

* [Patch 5517](#patch-5517)

## Patch 5517

✅ Verified (Client)

Located at `ini/FontSetting.ini`.

```ini
[FontSetting]
ChatFontSize=12
ChatFont=simsun.ttf
GUIFont=simsun.ttf
```

| Field          | Type   | Description                                                                               |
|:---------------|:-------|:------------------------------------------------------------------------------------------|
| `ChatFontSize` | int    | Size used for chat and floating text.                                                     |
| `ChatFont`     | string | Font filename in the client root, or an installed Windows font name, used for chat text.  |
| `GUIFont`      | string | Font filename in the client root, or an installed Windows font name, used for GUI labels. |
