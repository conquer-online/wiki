# ProfessionalName.ini

This file maps each `ProfessionType` identifier to its display name.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

☑️ Assumed (Soul)

### ProfessionType Structure

The leading digits identify the class and the trailing digit is the promotion rank within that class:

| Range   | Class   |
|:--------|:--------|
| 10 - 15 | Trojan  |
| 20 - 25 | Warrior |
| 40 - 45 | Archer  |
| 100+    | Taoist  |

### File Format

This is a plain-text file with one entry per line, comma-separated:

```
<ProfessionType>,<Name>
```

### Example Entries

| ProfessionType | Name          |
|:---------------|:--------------|
| 10             | InternTrojan  |
| 11             | Trojan        |
| 12             | VeteranTrojan |
| 13             | TigerTrojan   |
| 14             | DragonTrojan  |
| 15             | TrojanMaster  |
| 20             | InternWarrior |
| 21             | Warrior       |
| 22             | BrassWarrior  |
| 23             | SilverWarrior |
| 24             | GoldWarrior   |
| 25             | WarriorMaster |
| ...            | ...           |
