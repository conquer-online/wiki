# Network

This section documents network procedures and message types for client-server communication.

Conquer Online uses [TCP/IPv4](https://en.wikipedia.org/wiki/Transmission_Control_Protocol) for network communication between the game servers and client. Messages are received as a stream, and ordering must be preserved for the correct processing of requests. Message encryption relies on the previous message, either as a counter or using cipher feedback; therefore, if the messages are encrypted and decrypted out of order, the client and server will desynchronize.

## Protocol

Conquer Online uses [Little-endian](https://en.wikipedia.org/wiki/Endianness) for the byte ordering of words and multi-byte sequences. 

Games developed by TQ Digital Entertainment employ a custom binary protocol in this endianness, and contain a message header and sometimes a message footer. Messages are written to the binary protocol using custom encoding rules that change between versions of the client. These changes are documented in the [Messages](messages/README.d) section.

## Subsections

* [Messages](messages/README.d): Definitions for how the client and server communicate.
