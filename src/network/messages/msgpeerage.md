# MsgPeerage

This message is used entirely for the [Nobility](../../features/nobility.md) (aka peerage) system where players can donate silver or CPs to achieve a peerage rank (Knight, Earl, King etc.), increase battle power and appear on a leaderboard.

## Patch 5517 (Mac: 1029)

✅ **Verified**: This data was determined through reverse engineering the Mac Client Binary 1029 (same release date as PC 5517) and also reverse engineering the leaked server binaries (namely `Peerage.dll` in ZFServer) 


#### Message Definition

| Pos | Type     | Name                               | Description                                                          | Example |
|:----|:---------|:-----------------------------------|:---------------------------------------------------------------------|:--------|
| 0   | UInt16   | [MsgSize](index.md#message-header) | Size of message                                                      | -       |
| 2   | UInt16   | [MsgType](index.md#message-header) | Type of message                                                      | 2064    |
| 4   | UInt16   | PeerageActionType                  | Action subtype                                                       | -       |
| 6   | UInt16   | -                                  | Padding 🔵                                                           | 0       |
| 8   | Variable | Data                               | Action-specific payload, see [PeerageActionType](#peerageactiontype) | -       |

🔵 Padding here is intentional to align the data payload start to be offset 8 (`UInt64`)

##### PeerageActionType

| Val | Name          | Description                            | Sender | Data                                                                                                                                                                                       |
|:----|:--------------|:---------------------------------------|:-------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | SEND_DONATION | Hero donates silver or CPs             | Client | `Amount` (UInt64), `CurrencyType`🟣 (UInt16)                                                                                                                                               |
| 1   | SEND_DONATION | Server confirms hero's donation        | Server | Padding (UInt64), Padding (UInt64), Padding (UInt64), [`ContributeDonateInfoString`](#contributedonateinfostring) ([NetStringPacker](../stringpacker.md))                                  |
| 2   | LEADERBOARD   | Request a leaderboard page             | Client | `PageNumber` (UInt32)                                                                                                                                                                      |
| 2   | LEADERBOARD   | Return a leaderboard page              | Server | See [Leaderboard Response](#leaderboard-response)                                                                                                                                          |
| 3   | REFRESH_RANK  | Refresh hero's peerage rank & donation | Server | [Hero ID](../identifiers.md) (UInt32), Padding (UInt64), Padding (UInt64), Padding (UInt32), [`ContributeTipInfoString`](#contributetipinfostring) ([NetStringPacker](../stringpacker.md)) |
| 4   | QUERY_MINIMUM | Query minimum donation to be a rank    | Client | `SelectedPeerageRank` (UInt32)                                                                                                                                                             |
| 4   | QUERY_MINIMUM | Return minimum donation data           | Server | `RemainingDonationAmount` (UInt64), Padding (UInt32), `ExpectedLeaderboardPosition` (UInt32), `CurrentLeaderboardPosition` (UInt32)                                                        |

🟣 `CurrencyType` values: `0` = Silver, `1` = EMoney (CPs), `2` = Bound EMoney (CPs).

### Leaderboard Response

| Pos | Type                | Name                          | Description                                       | Example   |
|:----|:--------------------|:------------------------------|:--------------------------------------------------|:----------|
| 8   | UInt16              | CurrentVisibleLeaderboardPage | The visible page in the client leaderboard dialog | 2         |
| 10  | UInt16              | TotalLeaderboardPages         | Total pages for leaderboard dialog                | 5         |
| 12  | UInt32              | EntryCount                    | Number of entries in this message (the page)      | 10        |
| 16  | UInt32              | -                             | Padding                                           | 0         |
| 20  | UInt32              | -                             | Padding                                           | 0         |
| 24  | UInt32              | -                             | Padding                                           | 0         |
| 28  | UInt32              | -                             | Padding                                           | 0         |
| 32  | `Entry[EntryCount]` | `LeaderboardEntryStruct[]`    | Leaderboard entries                               | See below |

#### Leaderboard Entry Structure

Each entry is **always** 48 bytes.

| Offset | Type   | Name                                     | Description                                                                   |
|:-------|:-------|:-----------------------------------------|:------------------------------------------------------------------------------|
| 0      | UInt32 | [Hero ID](../identifiers.md)             | The player's unique identifier                                                |
| 4      | UInt8  | Hero Online                              | Boolean set to `1` if player is online (value is unused by the client)        |
| 5      | UInt8  | -                                        | Padding                                                                       |
| 6      | UInt16 | -                                        | Padding                                                                       |
| 8      | UInt32 | [Look Face](../../constants/lookface.md) | The player's mesh, to derive gender of the peerage rank                       |
| 12     | String | [HeroName](../../strings/heroname.md)    | Player's character name (16 bytes)                                            |
| 28     | UInt32 | -                                        | Padding                                                                       |
| 32     | Int64  | PlayerTotalDonation                      | The player's cumulative total donation amount                                 |
| 40     | UInt32 | PeerageRank                              | The player's peerage rank number, see [Nobility](../../features/nobility.md)  |
| 44     | Int32  | Position                                 | The player's position on the donation leaderboard (Start at 0, client adds 1) |

### ContributeDonateInfoString

`ContributeDonateInfoString` is a space-separated string parsed by the client as `"%u %u %lld %lld %u"`

| Index | Format | Name                         | Description                                                      |
|:------|:-------|:-----------------------------|:-----------------------------------------------------------------|
| 0     | UInt32 | [Hero ID](../identifiers.md) | The hero's UID                                                   |
| 1     | UInt32 | Unknown                      | Parsed but appears **unused** by the client                      |
| 2     | Int64  | DonationAmount               | The confirmed amount donated by the hero                         |
| 3     | Int64  | TotalDonation                | The hero's cumulative total donation amount                      |
| 4     | UInt32 | LeaderboardPosition          | The hero's donation leaderboard rank (Start at 0, client adds 1) |

### ContributeTipInfoString

`ContributeTipInfoString` is a space-separated string parsed by the client as `"%u %lld %u %d"`.

| Index | Format | Name                         | Description                                                                 |
|:------|:-------|:-----------------------------|:----------------------------------------------------------------------------|
| 0     | UInt32 | [Hero ID](../identifiers.md) | The hero's UID                                                              |
| 1     | Int64  | TotalDonation                | The hero's cumulative total donation amount                                 |
| 2     | UInt32 | PeerageRank                  | The hero's peerage rank number, see [Nobility](../../features/nobility.md)  |
| 3     | Int32  | LeaderboardPosition          | The hero's position on the donation leaderboard (Start at 0, client adds 1) |
