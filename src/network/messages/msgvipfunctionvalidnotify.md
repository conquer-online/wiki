# MsgVipFunctionValidNotify

This message is sent from the game server to the client to enable [VIP](../../features/vip.md) feature buttons in the VIP Dialog. The message contains a single bitwise flag that determines which VIP buttons are visible. The server should send this message during the login sequence while processing [MsgUserInfo](msguserinfo.md)

This message cannot be sent to the server by the client.

## Patch 5517 (Mac: 1029)

#### Message Definition

✅ **Verified (Client)**: Confirmed by reverse engineering the client binary Mac 1029 (same release date at PC 5517)

| Pos | Type   | Name                                      | Description                              | Example |
|:----|:-------|:------------------------------------------|:-----------------------------------------|:--------|
| 0   | UInt16 | [MsgSize](index.md#message-header)        | Size of the message                      | 8       |
| 2   | UInt16 | [MsgType](index.md#message-header)        | Type of message                          | 1129    |
| 4   | UInt32 | [VipFunctionFlags](../../features/vip.md) | Bitwise flag to show or hide VIP buttons | 0xFFFF  |
