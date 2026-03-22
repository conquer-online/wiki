# VipTrans.ini

This file defines the teleport destinations available to [VIP players](../../features/vip.md). It is read by the client to populate the City Teleport (VIP Level 2+) & Portal Teleport (VIP Level 3+) dialog buttons.

City Teleport is the major cities such as TwinCity, PhoenixCastle, ApeCity, DesertCity & BirdIsland

Portal Teleport is a section of the map, for example: `WindPlain-Turtledove` - for the Turtledove section of Windplain.

## File Format

Each line contains three space-separated fields:

```
<Index> <Group> <LocationName>
```

| Field | Type | Description |
|:------|:-----|:------------|
| Index | Int | The order within the group |
| Group | Int | `1` = City Teleport, `0` = Portal Teleport |
| LocationName | String | Name of the location |
