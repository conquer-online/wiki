# StrRes.ini

A key-value string resource file used by the client to look up UI text, system messages, and error strings by integer ID. Read at client startup.

## Table of Contents

* [Patch 5517](#patch-5517)

## Patch 5517

✅ Verified (Client)

Located at `ini/StrRes.ini`.

Each line is in the format:

```
<StringID>=<String>
```

String values may contain printf-style format specifiers (`%d`, `%s`, `%f`, `%I64u`) and escape sequences (`\n` for newline). Both English and GBK-encoded Chinese strings are supported in the same file.

### ID Ranges

A comment at the top of the file (written in Chinese) documents the intended ID ranges.

| Range           | Subsystem  |
|:----------------|:-----------|
| 10000 - 50000   | Interface  |
| 100000 - 200000 | 3DRole     |
| 300000 - 400000 | 3DGameMap  |
| 500000 - 600000 | 3DBaseCode |
