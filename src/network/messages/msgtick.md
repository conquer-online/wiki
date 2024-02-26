# MsgTick

This message is sent from the game server to the client, and then back again from the client to the game server in a round-trip for checking network congestion. The message is responsible for the "Warning: the network is congested" message that appears in the top-left of the client screen. It's secondary purpose is for verifying that the user is not a bot (Conquer 1.0 and early Conquer 2.0).

The timestamp sent with this message is XORed with the hero ID. The check data at the end of the message is a checksum of the first two characters of the hero's name. This appears as the following in COPSv7:

```c++
static uint32_t checksum(const char* aName)
{
    if (aName == nullptr || aName[0] == '\0' || strlen(aName) < 4)
        return UINT32_C(0x9D4B5703);
    else
    {
        uint16_t val = ((uint16_t*)aName)[0];
        #if BYTE_ORDER == BIG_ENDIAN
        val = bswap16(val);
        #endif // BYTE_ORDER == BIG_ENDIAN

        return val ^ UINT16_C(0x9823);
    }
}
```

## Table of Contents

* [Patch 5065](#patch-5065)

## Patch 5065

#### Message Definition

☑️ Assumed (Observed) - COPSv7 + Soul

| Pos | Type | Name | Description | Example |
|:-------|:--------|:--------|:--------|:--------|
| 0  | UInt16 | [MsgSize](index.md#message-header) | Size of the message | 20 |
| 2  | UInt16 | [MsgType](index.md#message-header) | Type of message | 1012 |
| 4  | UInt32 | [Hero ID](/network/identifiers.md) | Unique identifier for the character | 1000000 |
| 8  | UInt32 | [System Time](/network/timestamp.md) | Milliseconds of system uptime ^ Hero ID | 1579846705 |
| 12 | UInt32 | Message Count | The total number of messages sent | 12 |
| 16 | UInt32 | Check Data | Checksum using first two letters of the character's name | 2638960387 | 
