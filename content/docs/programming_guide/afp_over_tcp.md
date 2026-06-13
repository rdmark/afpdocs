---
title: "AFP Over TCP"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 16
---

# AFP Over TCP

This chapter describes how the Transmission Control Protocol (TCP) can
be used to transport AFP packets efficiently. With TCP as the transport
protocol, AFP services can be made available over the Internet just as
they are made over AppleTalk networks. When a user mounts a remote
volume over TCP, the type of network over which the volume is mounted is
completely transparent to the user. On local area networks, providing
AFP services over TCP/IP effectively utilizes the bandwidth of high
speed network media such as Fiber Distributed Data Interface (FDDI) and
Asynchronous Transfer Mode (ATM).

TCP can be used as the transport protocol for AFP version 2.1 and later.

## Implementation

A layer known as the Data Stream Interface (DSI) is used to provide AFP
services over TCP. With minimal overhead, the DSI establishes an
interface between AFP and TCP that is generic enough to be used over any
data stream protocol. The DSI has the following characteristics:

- It registers the AFP server on a well-known data stream port. For TCP,
  the port number is 548. Protocol suites that include a
  service-locating protocol (Bonjour, for example) can be used to
  advertise and locate an AFP server.

- It uses a request/response model that supports multiple outstanding
  requests on any given connection. In other words, the request’s window
  size may be greater than 1 in length.

- It replies to multiple outstanding requests in any order.

- It provides a one-to-one mapping between the AFP session and the port
  ID or connection ID maintained by the data stream protocol.

- It maintains some state information for every open client connection.
  This allows the server to demultiplex requests to an appropriate AFP
  session.

- It allows the AFP server to send and receive large packets. The size
  of the packets is based on the underlying network’s maximum
  transmission unit (MTU).

## DSI Commands

DSI commands are similar to ASP commands, and they preserve all of the
ASP commands except `ASPWriteContinue`. The DSI commands are listed in
Table 6-1.

| Command name      | Command code | Originator of command requests |
|-------------------|--------------|--------------------------------|
| `DSICloseSession` | `1`          | Client and server              |
| `DSICommand`      | `2`          | Client only                    |
| `DSIGetStatus`    | `3`          | Client only                    |
| `DSIOpenSession`  | `4`          | Client only                    |
| `DSITickle`       | `5`          | Client and server              |
| `DSIWrite`        | `6`          | Client only                    |
| `DSIAttention`    | `8`          | Server only                    |

**Table 6-1**  DSI commands

**Note:** For consistency between ASP and DSI commands, the command code
for DSIAttention is `8`.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/AFPOverTCP/AFPOverTCP.html)
and presented here strictly for archival purposes.
