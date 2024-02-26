# Identifiers

Unique identifiers in Conquer Online are 32-bit unsigned integers split into incremental ranges. Due to the small size of identifiers, some must be recycled and reused, such as monster identifiers. The easiest method of recycling these identifiers is to create reservations per spawn area.

> ⚠️ __WARNING__
>
> Incremental IDs, such as account IDs and item IDs, can be too predictable and lead to exposing account information of your PM / first created accounts on the server, or items in the database. Consider using a [linear-feedback shift register](https://en.wikipedia.org/wiki/Linear-feedback_shift_register) for a pseudo-random identifier that is deterministic for counting, but obfuscated for general security use.

## Table of Contents

* [Account Server](#account-server)
* [Game Server](#game-server)

## Account Server

Account IDs can be any number in the range of a 32-bit unsigned integer.

## Game Server

The game server has the following ranges statically defined.

| Min     | Max    | Name  | Description |
|:--------|:-------|:------|:--------|
| 0000001 | 0000299999 | Scene | Scenery NPC |
| 0000001 | 0000099999 | System NPC | Statically spawned NPC |
| 0100001 | 0000199999 | Dynamic NPC | Dynamically spawned NPC |
| 0400001 | 0000499999 | Monster | World monster spawn |
| 0500001 | 0000599999 | Pet | Syndicate monster spawn |
| 0700001 | 0000799999 | Call Pet | Player monster spawn |
| 0900001 | 0000989999 | Magic Trap | Player spell trap from [MsgMapItem](/network/messages/msgmapitem.md) |
| 0990001 | 0000999999 | System Trap | System trap from [MsgMapItem](/network/messages/msgmapitem.md) |
| 1000000 | 3999999999 | Hero | Player character |

Some identifiers, such as items, are incremental across a 32-bit unsigned integer range.