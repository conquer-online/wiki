# MsgDice

One of the first street gambling games introduced in Conquer Online was the dice game hosted by DiceKing in the Market. The game revolves around the NPC rolling four dice and the player making bets on the outcome. The outcome can be high or low, three of a kind, or specific values.

Interestingly, results of the game are broadcast to all participants using the [MsgName](msgname.md) message rather than a server message via [MsgTalk](msgtalk.md). MsgName is also used to add players to the game.

The game is split into three phases: a 30 second phase where players can bet (Amount is set to 30 for BEGINCHIP), followed by a 5 second phase where all bets are in (ENDCHIP), followed by the result (DICE).

## Table of Contents

* [Patch 4267](#patch-4267)

## Patch 4267

#### Message Definition

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 20 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1113 |
| 4 | Byte | [Action](#action-type) | How to processes the message | 0 |
| 5 | Byte | Amount | Amount of data or time | 1 |
| 6 | UInt32 | NPC ID | [Role ID](../identifiers.md) of the NPC | 169 |
| 10 | Struct | [DiceData](#dice-data) | Payload for dices | |

#### Action Type

☑️ Assumed (Soul)

| Val | Name | Description | Recipient |
|:------|:--------|:--------|:--------|
| 0 | CHIPIN | Shows a new bet | Both |
| 1 | CHIPIN_CONFIRM | Confirms a bet | Client |
| 2 | CANCELCHIP | Removes a bet | Both |
| 3 | CANCELCHIP_CONFIRM | Confirms removal | Client |
| 4 | BEGINCHIP | Start a betting window | Client |
| 5 | ENDCHIP | Stops betting window | Client |
| 6 | DICE | Results of the role | Client |

#### Dice Data

☑️ Assumed (Soul)

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0 | Byte | Type | [Dice Value](#dice-values) for betting | 1 |
| 1 | UInt32 | Data | Amount of money or array of dice | 1000 |


#### Dice Values

☑️ Assumed (Soul)

```proto
enum DiceValues {

    DICE_VALUE_SMALL = 0;
    DICE_VALUE_BIG = 1;
    DICE_VALUE_111 = 2;
    DICE_VALUE_222 = 3;
    DICE_VALUE_333 = 4;
    DICE_VALUE_444 = 5;
    DICE_VALUE_555 = 6;
    DICE_VALUE_666 = 7;
    DICE_VALUE_4 = 8;
    DICE_VALUE_5 = 9;
    DICE_VALUE_6 = 10;
    DICE_VALUE_7 = 11;
    DICE_VALUE_8 = 12;
    DICE_VALUE_9 = 13;
    DICE_VALUE_10 = 14;
    DICE_VALUE_11 = 15;
    DICE_VALUE_12 = 16;
    DICE_VALUE_13 = 17;
    DICE_VALUE_14 = 18;
    DICE_VALUE_15 = 19;
    DICE_VALUE_16 = 20;
    DICE_VALUE_17 = 21;
    DICE_VALUE_ALL = 22;
}
```