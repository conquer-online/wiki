# MapMagicItem.ini

This file is loaded on client role data initialization, and utilized by [MsgMapItem](/network/messages/MsgMapItem.md) to show magical effects on the map floor. These effects play as "moments" that the client iterates through: starting with "start" and ending with "end". If any of the moment [TMEs](/files/formats/tme.md) are "0" in the file, then that moment will be skipped.

The "look" described in [MsgMapItem](/network/messages/MsgMapItem.md) is the type key in the INI file.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

☑️ Assumed (Soul)

| Field | Type | Description | Example |
|:-------|:--------|:--------|:--------|
| Start | String | Starting [TME](/files/formats/tme.md) to play at start of processing | rain01.TME |
| Last | String | Lasting [TME](/files/formats/tme.md) playing until effect is removed | windblade7-1.TME |
| End | String | Ending [TME](/files/formats/tme.md) to play at the end of processing | line05.TME |

Below is an example entry using the definition above:

```ini
[Type10]
Start=rain01.TME
Last=windblade7-1.TME
End=line05.TME
```
