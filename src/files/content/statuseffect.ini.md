# StatusEffect.ini

This file is used to map effects to player statuses for [MsgUserInfo](/network/messages/msguserinfo.md). The index mapping can be found on that page, but the file structure for mapping those effects can be found below. Though labeled as an INI file, it doesn't follow the syntax. Each entry is space delimitated and line separated.

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

✅ Verified (Client)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0 | Int64 | Index | Status index | 1 |
| 1 | Char[64] | 3DEffect | 3D effect name | poisonstate |
| 2 | Char[64] | 2DEffect | 2D effect name | NULL |
