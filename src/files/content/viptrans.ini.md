# VipTrans.ini

This file defines the teleport destinations available to [VIP players](../../features/vip.md). It is read by the client to populate the City Teleport (VIP Level 2+) & Portal Teleport (VIP Level 3+) dialog buttons.

City Teleport is the major cities such as TwinCity, PhoenixCastle, ApeCity, DesertCity & BirdIsland

Portal Teleport is a section of the map, for example: `WindPlain-Turtledove` - for the Turtledove section of Windplain.

## Table of Contents

* [Patch 5517](#patch-5517)

## Patch 5517

✅ Verified (Client)

Each line contains three space-separated fields:

```
<Index> <Group> <LocationName>
```

| Field          | Type   | Description                                  |
|:---------------|:-------|:---------------------------------------------|
| `Index`        | int    | The order within the group                   |
| `Group`        | int    | `1` = City Teleport, `0` = Portal Teleport   |
| `LocationName` | string | Name of the location                         |
