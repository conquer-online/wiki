# MsgPlayerAttribInfo

This message is sent to the client to initialize the battle statistics panel with various damage and defense attributes, and is sent after the [MsgUserInfo](msguserinfo.md) and [MsgItemInfo](msgiteminfo.md) messages to finish displaying equipped items. When a player's equipment is observed by another player using [MsgAction](msgaction.md), then this message is also sent to finish populating equipment.

New attributes were introduced with the introduction of Refinery, Stabilization, and Chi.

## Table of Contents

* [Patch 5615](#patch-5615)

## Patch 5615

#### Message Definition

❓ Unverified

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 136 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1040 |
| 4  | UInt32 | [Hero ID](../identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | UInt32 | Life | Current hitpoints | 100 |
| 12 | UInt32 | Mana | Current mana points | 0 |
| 16 | UInt32 | MaxAttack | [Physical max attack](../../algorithms/calculations/damage.md) before modifiers | 7 |
| 20 | UInt32 | MinAttack | [Physical min attack](../../algorithms/calculations/damage.md) before modifiers | 14 |
| 24 | UInt32 | Defense | Effective [defense](../../algorithms/calculations/damage.md) before modifiers | 32 |
| 28 | UInt32 | MagicAttack | [Magic attack](../../algorithms/calculations/damage.md) modifier | 0 |
| 32 | UInt32 | MagicDefense | [Magic defense](../../algorithms/calculations/damage.md) modifier | 0 |
| 36 | UInt32 | DodgePercent | [Dodge](../../algorithms/calculations/damage.md) increase | 92 |
| 40 | UInt32 | Agility | Raw [agility attribute](../../algorithms/calculations/attributes.md) | 20 |
| 44 | UInt32 | Accuracy | Hit rate [accuracy](../../algorithms/calculations/attributes.md) | 10 |
| 48 | UInt32 | BonusAttackPercent | [Physical attack](../../algorithms/calculations/damage.md) increase | 0 |
| 52 | UInt32 | BonusMagicPercent | [Magic attack](../../algorithms/calculations/damage.md) increase | 0 |
| 56 | UInt32 | ReduceDamagePercent | Overall [damage](../../algorithms/calculations/damage.md) reduction | 7 |
| 60 | UInt32 | CurseDamagePercent | Cursed [damage](../../algorithms/calculations/damage.md) increase | 0 |
| 64 | UInt32 | BlessPercent | Bless [damage](../../algorithms/calculations/damage.md) reduction | 0 |
| 68 | UInt32 | CriticalStrikePercent | Physical [critical hit](../../algorithms/calculations/damage.md) increase | 0 |
| 72 | UInt32 | MagicCriticalStrikePercent | Magic [critical hit](../../algorithms/calculations/damage.md) increase | 0 |
| 76 | UInt32 | ImmunityPercent | [Critical hit](../../algorithms/calculations/damage.md) negation increase | 0 |
| 80 | UInt32 | PenetrationPercent | [Magic defense](../../algorithms/calculations/damage.md) negation | 0 |
| 84 | UInt32 | BlockPercent | Physical [damage](../../algorithms/calculations/damage.md) block | 0 |
| 88 | UInt32 | BreakthroughPercent | [Max attack](../../algorithms/calculations/damage.md) increase for higher BP | 0 |
| 92 | UInt32 | CounteractionPercent | Breakthrough counteraction | 0 |
| 96 | UInt32 | DetoxicationPercent | [Poison attack](../../algorithms/calculations/damage.md) reduction | 0 | 
| 100 | UInt32 | FinalAttack | Final [physical attack](../../algorithms/calculations/damage.md) increase | 7 |
| 104 | UInt32 | FinalMagicAttack | Final [magic attack](../../algorithms/calculations/damage.md) increase | 0 |
| 108 | UInt32 | FinalDefense | Final [physical attack](../../algorithms/calculations/damage.md) reduction | 32 |
| 112 | UInt32 | FinalMagicDefense | Final [magic attack](../../algorithms/calculations/damage.md) reduction | 0 |
| 116 | UInt32 | MetalResistPercent | Metal boss [damage](../../algorithms/calculations/damage.md) reduction | 0 |
| 120 | UInt32 | WoodResistPercent | Wood boss [damage](../../algorithms/calculations/damage.md) reduction | 0 |
| 124 | UInt32 | WaterResistPercent | Water boss [damage](../../algorithms/calculations/damage.md) reduction | 0 |
| 128 | UInt32 | FireResistPercent | Fire boss [damage](../../algorithms/calculations/damage.md) reduction | 0 |
| 132 | UInt32 | EarthResistPercent | Earth boss [damage](../../algorithms/calculations/damage.md) reduction | 0 |