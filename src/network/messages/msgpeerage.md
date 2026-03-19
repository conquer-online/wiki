# MsgPeerage

This message is used entirely for the [Nobility](../../features/nobility.md) (aka peerage) system where players can donate silver or CPs to achieve a peerage rank, increase battle power and appear on a leaderboard.

## Patch 5517 (Mac: 1029)

❓ **Observed**: Determined through reverse engineering the Mac Client Binary 1029 (same release date as PC 5517), some server-side implementation & then the observing client behavior. Due to the significant trial and error involved, some details may be inaccurate.

This message is used for both client-to-server and server-to-client communication, each with their own set of subtypes of this message type.

After the standard [Message Header](index.md#message-header) there is a `UInt16` value which we'll call 'Subtype'. Subtype can be 1 to 4 inclusive. When the client processes the message, a conditional uses the value of the subtype to determine the remaining message fields & action to take. Subtype 1, 2 & 4 are first sent by the client and a message of the same subtype is returned by the server as a response.


### Subtype 1 - Send Donation 

This message subtype is first sent by the client when the hero makes a donation. The server responds with the same message subtype, confirming the donation (a dialog appears client-side)

#### Send Donation Message Definition (Client -> Server)

| Pos | Type   | Name                               | Description                                                                    | Example  |
|:----|:-------|:-----------------------------------|:-------------------------------------------------------------------------------|:---------|
| 0   | UInt16 | [MsgSize](index.md#message-header) | Size of message                                                                | 56       |
| 2   | UInt16 | [MsgType](index.md#message-header) | Type of message                                                                | 2064     |
| 4   | UInt16 | Subtype                            | Action type                                                                    | 1        |
| 6   | UInt16 | Unknown                            | Likely Padding                                                                 | -        |
| 8   | UInt64 | Amount                             | Contribution amount                                                            | 30000000 |
| 16  | UInt16 | CurrencyType                       | Currency used to donate (0 = Silver, 1 = Bound EMoney (CPs), 2 = EMoney (CPs)) | 0        |

#### Send Donation Response Message Definition (Server -> Client)

| Pos | Type                                  | Name                               | Description                        | Example               |
|:----|:--------------------------------------|:-----------------------------------|:-----------------------------------|:----------------------|
| 0   | UInt16                                | [MsgSize](index.md#message-header) | Size of message                    | 58                    |
| 2   | UInt16                                | [MsgType](index.md#message-header) | Type of message                    | 2064                  |
| 4   | UInt16                                | Subtype                            | Action type                        | 1                     |
| 6   | UInt16                                | Unknown                            | Likely padding                     | -                     |
| 8   | UInt64                                | Unknown                            | Likely padding                     | -                     |
| 16  | UInt64                                | Unknown                            | Likely padding                     | -                     |
| 24  | UInt64                                | Unknown                            | Likely padding                     | -                     |
| 32  | [NetStringPacker](../stringpacker.md) | ContributeDonateInfoString         | Space-separated string (see below) | 0 0 3000000 9000000 0 |

`ContributeDonateInfoString` is a space-separated string passed to the function `SetContributeDonateInfo`, which parses it as `"%u %u %lld %lld %u"`. These values are stored on the hero object and read by the dialog `DlgContributeConfirm` (StrRes: 11112, 11113, 11602) to display the donation confirmation:

| Index | Format | Name                         | Description                                    |
|:------|:-------|:-----------------------------|:-----------------------------------------------|
| 0     | UInt32 | [Hero ID](../identifiers.md) | The hero's UID                                 |
| 1     | UInt32 | Unknown                      | Parsed but appears unused by the client        |
| 2     | Int64  | DonationAmount               | The confirmed amount donated by the hero       |
| 3     | Int64  | TotalDonation                | The hero's cumulative total donation amount    |
| 4     | UInt32 | LeaderboardPosition          | The hero's donation leaderboard rank (Start 0) |

### Subtype 2 - Leaderboard

This message is used to request and display the donation leaderboard. It is a paginated request.

#### Leaderboard Pagination Message Definition (Client -> Server)

| Pos | Type   | Name                               | Description                          | Example |
|:----|:-------|:-----------------------------------|:-------------------------------------|:--------|
| 0   | UInt16 | [MsgSize](index.md#message-header) | Size of message                      | 28      |
| 2   | UInt16 | [MsgType](index.md#message-header) | Type of message                      | 2064    |
| 4   | UInt16 | Subtype                            | Action type                          | 2       |
| 6   | UInt16 | Unknown                            | Likely Padding                       | -       |
| 8   | UInt32 | PageNumber                         | Requested leaderboard page (Start 0) | 0       |

#### Leaderboard Pagination Response Message Definition (Server -> Client)

| Pos | Type              | Name                               | Description                                       | Example   |
|:----|:------------------|:-----------------------------------|:--------------------------------------------------|:----------|
| 0   | UInt16            | [MsgSize](index.md#message-header) | Size of message                                   | 512       |
| 2   | UInt16            | [MsgType](index.md#message-header) | Type of message                                   | 2064      |
| 4   | UInt16            | Subtype                            | Action type                                       | 2         |
| 6   | UInt16            | Unknown                            | Likely Padding                                    | -         |
| 8   | UInt16            | CurrentVisibleLeaderboardPage      | The visible page in the client leaderboard dialog | 2         |
| 10  | UInt16            | TotalLeaderboardPages              | Number of total pages for leaderboard dialog      | 5         |
| 12  | UInt32            | EntryCount                         | Number of entries in this message (the page)      | 10        |
| 16  | UInt32            | Unknown                            | Likely Padding                                    | -         |
| 20  | UInt32            | Unknown                            | Likely Padding                                    | -         |
| 24  | UInt32            | Unknown                            | Likely Padding                                    | -         |
| 28  | UInt32            | Unknown                            | Likely Padding                                    | -         |
| 32  | Entry[EntryCount] | LeaderboardEntryStruct[]           | Leaderboard Entries                               | See Below |

##### Leaderboard Entry Structure

The total size of this structure is always 48 bytes.

| Offset | Type   | Name                                     | Description                                                                  |
|:-------|:-------|:-----------------------------------------|:-----------------------------------------------------------------------------|
| 0      | UInt32 | [PlayerUID](../identifiers.md)           | The player's UID                                                             |
| 4      | UInt8  | Unknown                                  | Parsed but appears unused by the client                                      |
| 5      | UInt8  | Unknown                                  | Likely Padding                                                               |
| 6      | UInt16 | Unknown                                  | Likely Padding                                                               |
| 8      | UInt32 | [Look Face](../../constants/lookface.md) | The player's mesh, to derive gender of the peerage rank                      |
| 12     | String | PlayerName                               | Player's character name (16 bytes)                                           |
| 28     | UInt32 | Unknown                                  | Parsed but appears unused by the client                                      |
| 32     | Int64  | PlayerTotalDonation                      | The player's cumulative total donation amount                                |
| 40     | UInt32 | PeerageRank                              | The player's peerage rank number, see [Nobility](../../features/nobility.md) |
| 44     | Int32  | Position                                 | The player's position on the donation leaderboard (Start 0)                  |

### Subtype 3 - Refresh Hero's Peerage Rank & Status Icon

#### Status Icon & Peerage Rank Message Definition (Server -> Client)

Refreshes the hero's peerage status icon & 3DEffect.

| Pos | Type                                  | Name                               | Description                         | Example       |
|:----|:--------------------------------------|:-----------------------------------|:------------------------------------|:--------------|
| 0   | UInt16                                | [MsgSize](index.md#message-header) | Size of message                     | 47            |
| 2   | UInt16                                | [MsgType](index.md#message-header) | Type of message                     | 2064          |
| 4   | UInt16                                | Subtype                            | Action type                         | 3             |
| 6   | UInt16                                | Unknown                            | Likely padding                      | -             |
| 8   | UInt32                                | [Hero ID](../identifiers.md)       | Unique identifier for the character | 1000000       |
| 12  | UInt64                                | Unknown                            | Likely padding                      | -             |
| 20  | UInt64                                | Unknown                            | Likely padding                      | -             |
| 28  | UInt32                                | Unknown                            | Likely padding                      | -             |
| 32  | [NetStringPacker](../stringpacker.md) | ContributeTipInfoString            | Space-separated string (see below)  | 1000000 0 7 0 |

ContributeTipInfoString is a space-separated string passed to the function `SetContributeTipInfo` which parses it as `%u %lld %u %d`. The values of the string are:

| Index | Format | Name                         | Description                                                                |
|:------|:-------|:-----------------------------|:---------------------------------------------------------------------------|
| 0     | UInt32 | [Hero ID](../identifiers.md) | The hero's UID                                                             |
| 1     | Int64  | TotalDonation                | The hero's cumulative total donation amount                                |
| 2     | UInt32 | PeerageRank                  | The hero's peerage rank number, see [Nobility](../../features/nobility.md) |
| 3     | Int32  | LeaderboardPosition          | The hero's position on the donation leaderboard (Start 0)                  |


Note, unlike the other subtypes - the client does not send this message subtype.

### Subtype 4 - Query Minimum

The hero can click buttons on the dialog which shows how much silver they need to donate to achieve that rank.

#### Query Minimum Message Definition (Client -> Server)

| Pos | Type   | Name                               | Description                                                                                           | Example |
|:----|:-------|:-----------------------------------|:------------------------------------------------------------------------------------------------------|:--------|
| 0   | UInt16 | [MsgSize](index.md#message-header) | Size of message                                                                                       | 80      |
| 2   | UInt16 | [MsgType](index.md#message-header) | Type of message                                                                                       | 2064    |
| 4   | UInt16 | Subtype                            | Action type                                                                                           | 4       |
| 6   | UInt16 | Unknown                            | Likely Padding                                                                                        | -       |
| 8   | UInt32 | SelectedPeerageRank                | The rank number clicked on the Minimum Donation by player, see [Nobility](../../features/nobility.md) | 7       |

#### Query Minimum Response Message Definition (Server -> Client)

| Pos | Type   | Name                               | Description                               | Example |
|:----|:-------|:-----------------------------------|:------------------------------------------|---------|
| 0   | UInt16 | [MsgSize](index.md#message-header) | Size of message                           | 28      |
| 2   | UInt16 | [MsgType](index.md#message-header) | Type of message                           | 2064    |
| 4   | UInt16 | Subtype                            | Action type                               | 4       |
| 6   | UInt16 | Unknown                            | Likely Padding                            | -       |
| 8   | UInt64 | RemainingDonationAmount            | Minimum donation hero needs for the rank  | 4300000 |
| 16  | UInt32 | Unknown                            | Likely Padding                            | -       |
| 20  | UInt32 | ExpectedLeaderboardPosition        | Leaderboard position for the queried rank | 60      |
| 24  | UInt32 | CurrentLeaderboardPosition         | The hero's current leaderboard position   | 50      |
