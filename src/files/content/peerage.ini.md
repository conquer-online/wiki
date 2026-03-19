# Peerage.ini

This file defines the icons & 3DEffects for the [Nobility](../../features/nobility.md) system.

## File Format

### INI Headings
The ini-heading is a number that follows the formula
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

For example, ini-heading `[72]` is the female (2) version of the 7th Rank (70) = Duchess

### INI Sections

Each ini-section defines the rank for that specific gender. Each ini-section has the following:

```
[71]
Name= Name of rank used in various places during string formatting
Icon16= Small DDS Icon (data/interface/Style01/nobility) for the rank in leaderboard
Icon32= Medium DDS Icon (data/interface/Style01/nobility) for the rank in leaderboard
Icon64= Large DDS Icon (data/interface/Style01/nobility) for the rank in leaderboard
Font16= Small DDS Glowing Text (data/interface/Style01/nobility) for the rank in leaderboard
Font32= Medium DDS Glowing Text (data/interface/Style01/nobility) for the rank in leaderboard
Font64= Large DDS Glowing Text (data/interface/Style01/nobility) for the rank in leaderboard
StatusIconID= The status button icon for the rank (define in StatusTips.ini -> data/pic/Contribute)
StatusIconEffect= Glowing Status Icon found in C3 (c3/effect/other/rank)
Effect1= The Text 3D Effect that appears on the hero found in C3 (c3/effect/other/rank/letter)
Effect2= The Crown Effect that appears on the hero found in C3 (c3/effect/other/rank/coronet)
Button= The button for the rank in the Contribute Dialog (defined in Control.ani -> data/interface/Style01/checontribute)
ChatIcon= The rank icon that appears in the whisper chat window with the hero (defined in chatContribute.ani -> data/interface/Style01/chatsystem/nobility_JPG)
ChatFont= The name for the rank that appears in the whisper chat window with the hero (defined in chatContribute.ani -> data/interface/Style01/chatsystem/nobility_JPG)
```
