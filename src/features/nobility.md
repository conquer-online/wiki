# Nobility (Peerage)

> ⚠️ __WARNING__
>
> The document is written by observing client patch 5517. There may be significant differences between client patches.

A player can donate silver or CPs (Conquer Points) to earn nobility on the server. It was introduced in patch 5017, with gender-specific ranks added in patch 5302. Depending on how much the player donates in total, their hero name can appear on a leaderboard, they get an increase in battle power & 3DEffect appears on their character model each time they are [loaded into view](../renderers/hero.md).

## Peerage Ranks

The table below shows the peerage ranks & the official requirements. Coincidentally, the rank number is also the same value as the increase in battle power. 

| Rank Number | Title             | Max Per Server | Requirement            |
|:------------|:------------------|:---------------|:-----------------------|
| 12          | King / Queen      | 3              | Leaderboard Rank 1-3   |
| 9           | Prince / Princess | 12             | Leaderboard Rank 4-15  |
| 7           | Duke / Duchess    | 35             | Leaderboard Rank 16-50 |
| 5           | Earl / Countess   | No Limit       | 200,000,000 silvers    |
| 3           | Baron / Baroness  | No Limit       | 100,000,000 silvers    |
| 1           | Knight / Lady     | No Limit       | 30,000,000 silvers     |
| 0           | Commoner          | N/A            | N/A                    |

Nobility titles, status button and effects are all defined in the file [peerage.ini](../files/content/peerage.ini.md) with the ini-heading formula calculated by:

```
(Rank Number * 10) + Gender   (1=Male 2= Female)
```

For example, ini-heading `[72]` in [peerage.ini](../files/content/peerage.ini.md) is the female version of the 7th Rank (Duchess) 

## Client Implementation

### Status Button

The hero's peerage rank should be sent by the server to the client shortly after the game server initializes the hero (after [MsgUserInfo](../network/messages/msguserinfo.md)) by sending the message [MsgPeerage: REFRESH_RANK](../network/messages/msgpeerage.md). This message is required for the nobility status button to appear, even if the hero has never donated (as they will be Rank Commoner).

The nobility status icon has a hover-over tooltip with the hero's total donation amount, their nobility rank and position on the leaderboard. The values of this tooltip come from the [MsgPeerage: REFRESH_RANK](../network/messages/msgpeerage.md) payload. If the hero has not achieved a rank then their rank is displayed as `--`.

### Submitting Donation

After clicking the nobility status button, the dialog `DlgContribution` appears. There is a field where the player can enter the amount of silver to donate. The minimum amount of silver is 3,000,000 (hardcoded in the client binary). After clicking submit, the player is prompted whether they wish to donate using CPs (Bound CPs are used first, then Non-Bound) instead of silver, where 1CP is equivalent to 50,000 silver (hardcoded in the client binary). After confirming the donation currency, the client sends the message [MsgPeerage: SEND_DONATION](../network/messages/msgpeerage.md) with the donation amount & currency-type.

There is client-side validation to ensure the hero has enough currency before submitting the donation, but the server should also validate and action the request. The server replies back with [MsgPeerage: SEND_DONATION](../network/messages/msgpeerage.md) to confirm the donation amount, the hero's total donation, and, if applicable, the hero's new position on the leaderboard.

The server should also send [MsgPeerage: REFRESH_RANK](../network/messages/msgpeerage.md) again to refresh the hero's status icon & rank. 

### Query Minimum Amount

On the Nobility Contribution dialog (`DlgContribution`) there is a section 'Minimum Donation', where the player can click on a button for each and any rank higher than their current peerage rank. When they click on a rank button, the client sends [MsgPeerage: QUERY_MINIMUM](../network/messages/msgpeerage.md) with the rank number clicked on. 

The server then calculates the minimum amount of silver the hero must donate for that rank and responds with [MsgPeerage: QUERY_MINIMUM](../network/messages/msgpeerage.md) with the rank number clicked on.

### Leaderboard 

> ❗ __IMPORTANT__
>
> Leaderboard positions are zero-indexed. The top donor (rank 1) is sent as position 0 by the server, and the client adds 1 to this.

On the Nobility Contribution dialog (`DlgContribution`) the top 5 most-donated players are shown. The client requests the top 5 players by sending [MsgPeerage: LEADERBOARD](../network/messages/msgpeerage.md) and the server responds with the same message with an array of the top 5 players' details.

The player can also select 'More' on the leaderboard, which will be a paginated list of top donated players. The client sends the requested page via [MsgPeerage: LEADERBOARD](../network/messages/msgpeerage.md) and the server responds back with [MsgPeerage: LEADERBOARD](../network/messages/msgpeerage.md).
