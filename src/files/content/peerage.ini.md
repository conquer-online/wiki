# Peerage.ini

This file defines the icons & 3DEffects for the [Nobility](../../features/nobility.md) system.

## Table of Contents

* [Patch 5517](#patch-5517)

## Patch 5517

✅ Verified (Client)

The ini-heading is a number that follows the formula:

```
(Rank Number * 10) + Gender
```

Gender (calculated by the client from the hero's mesh) is 1 for Male or 2 for Female.

The Peerage ranks are:

| Rank Number | Title             |
|:------------|:------------------|
| 12          | King / Queen      |
| 9           | Prince / Princess |
| 7           | Duke / Duchess    |
| 5           | Earl / Countess   |
| 3           | Baron / Baroness  |
| 1           | Knight / Lady     |
| 0           | Commoner          |

For example, ini-heading `[72]` is the female (2) version of the 7th Rank (70) = Duchess.

Below is an example entry using the definition above:

```ini
[71]
Name=Duke
Icon16=nob_Marquis16
Icon32=nob_Marquis32
Icon64=nob_Marquis64
Font16=nob_MarquisFont16
Font32=nob_MarquisFont32
Font64=nob_MarquisFont64
StatusIconID=40
StatusIconEffect=InsigniaNoble05s
Effect1=letter5
Effect2=coronet2
Button=checont_shiremarquis
ChatIcon=nob_MarquisJPG
ChatFont=nob_MarquisFontJPG
```

| Field              | Type   | Description                                                                                                                                  |
|:-------------------|:-------|:---------------------------------------------------------------------------------------------------------------------------------------------|
| `Name`             | string | Display name of the rank used in various places during string formatting                                                                     |
| `Icon16`           | string | Small DDS icon for the rank in the leaderboard (`data/interface/Style01/nobility`)                                                           |
| `Icon32`           | string | Medium DDS icon for the rank in the leaderboard (`data/interface/Style01/nobility`)                                                          |
| `Icon64`           | string | Large DDS icon for the rank in the leaderboard (`data/interface/Style01/nobility`)                                                           |
| `Font16`           | string | Small DDS glowing text for the rank in the leaderboard (`data/interface/Style01/nobility`)                                                   |
| `Font32`           | string | Medium DDS glowing text for the rank in the leaderboard (`data/interface/Style01/nobility`)                                                  |
| `Font64`           | string | Large DDS glowing text for the rank in the leaderboard (`data/interface/Style01/nobility`)                                                   |
| `StatusIconID`     | uint   | Status button icon ID for the rank. Defined in `StatusTips.ini` (`data/pic/Contribute`)                                                      |
| `StatusIconEffect` | string | Glowing status icon in C3 (`c3/effect/other/rank`)                                                                                           |
| `Effect1`          | string | Text 3D effect that appears on the hero in C3 (`c3/effect/other/rank/letter`)                                                                |
| `Effect2`          | string | Crown effect that appears on the hero in C3 (`c3/effect/other/rank/coronet`)                                                                 |
| `Button`           | string | Button for the rank in the Contribute Dialog. Defined in [Control.ani](../content/control.ani.md) (`data/interface/Style01/checontribute`)   |
| `ChatIcon`         | string | Rank icon in the whisper chat window. Defined in [chatContribute.ani](chatContribute.Ani) (`data/interface/Style01/chatsystem/nobility_JPG`) |
| `ChatFont`         | string | Rank name in the whisper chat window. Defined in [chatContribute.Ani](chatContribute.Ani) (`data/interface/Style01/chatsystem/nobility_JPG`) |
