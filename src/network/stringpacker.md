# NetStringPacker

As stated on the [Network](index.md) overview page, Conquer Online uses a custom binary protocol in [Little-endian](https://en.wikipedia.org/wiki/Endianness). In order to send a string over the protocol, Conquer Online will either use a fixed length character buffer or prefix the string with a byte length.

TQ Digital Entertainment's NetStringPacker is a collection of byte length prefixed strings, prefixed by the total size of the collection (also represented as a byte).

## Structure

| Type | Name | Description |
| ---- | ---- | ----------- |
| Byte | Amount | Total number of strings |
| PString[] | Strings | Array of length-prefixed strings |

## Example

The following example is from [MsgTalk](messages/msgtalk.md).

| Pos | Type | Name | Description | Example |
| --- | ---- | ---- | ----------- | ------- |
| 0 | Byte | Amount | Total number of strings | 4 |
| 1 | Byte | Length | Length of the first string | 6 |
| 2 | Char[6] | Speaker | Author of the message | SYSTEM |
| 8 | Byte | Length | Length of the second string | 8 |
| 9 | Char[8] | Header | Recipient of the message | ALLUSERS |
| 17 | Byte | Length | Length of the third string | 0 |
| 18 | Byte | Length | Length of the fourth string | 7 |
| 19 | Char[7] | Words | The body of the message | Testing | 

The total size of this NetStringPacker is 26 bytes.