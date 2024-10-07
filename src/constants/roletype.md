# Role Type

Roles in Conquer Online are entities such as [NPCs](../renderers/npc.md), [Monsters](../renderers/monster.md), and [Heroes](../renderers/hero.md) (the players). Depending on the role, the game client interprets left click actions differently. The server may use these constants to determine how [MsgInteract](../network/messages/msginteract.md) is processed, or how an NPC is spawned using [MsgNpcInfo](../network/messages/msgnpcinfo.md).

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

☑️ Assumed (Soul)

```proto
enum RoleType {

    ROLE_NPC_NONE = 0;
    ROLE_SHOPKEEPER_NPC = 1;
    ROLE_TASK_NPC = 2;
    ROLE_STORAGE_NPC = 3;
    ROLE_TRUNK_NPC = 4;
    ROLE_FACE_NPC = 5;
    ROLE_FORGE_NPC = 6;
    ROLE_EMBED_NPC = 7;
    ROLE_STATUARY_NPC = 9;
    ROLE_SYNFLAG_NPC = 10;

    ROLE_PLAYER = 11,
    ROLE_HERO = 12,
    ROLE_MONSTER = 13,

    ROLE_BOOTH_NPC = 14,
    SYN_TRANSPORT_NPC = 15,
    ROLE_BOOTH_FLAG_NPC = 16,
    ROLE_MOUSE_NPC = 17,
    ROLE_MAGICITEM = 18,
    ROLE_DICE_NPC = 19,
    ROLE_WEAPONGOAL_NPC = 21,
    ROLE_MAGICGOAL_NPC = 22,
    ROLE_BOWGOAL_NPC = 23,
    ROLE_TARGET_NPC = 24,
    ROLE_FURNITURE_NPC = 25,
    ROLE_CITY_GATE_NPC = 26,
    ROLE_NEIGHBOR_DOOR = 27,
    ROLE_CALL_PET = 28,
    TRAINPLACE_NPC = 29,
    AUCTION_NPC = 30,
    ROLE_STONE_MINE = 31,
    ROLE_PKGAME_NPC = 32,
    ROLE_3DFURNITURE_NPC = 101,
    ROLE_CITY_WALL_NPC = 102,
    ROLE_CITY_MOAT_NPC = 103,
}
```