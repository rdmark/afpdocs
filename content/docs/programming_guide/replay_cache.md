---
title: "AFP Replay Cache"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 17
---

# AFP Replay Cache

If the server supports the replay cache, then in the `DSIOpenSession`
reply packet from the server, there is a new option type of
`kServerReplayCacheSize`. The *Option* field length is 4 bytes, and the
*Option* value is the maximum number of DSI requests that the AFP server
can cache in its replay cache. The client selects the smaller of its own
maximum size or the server’s maximum size.

On the server side, the replay cache is the same size as the client’s
replay cache so you can free the oldest DSI request when you receive a
request with ID `size+1`.

For example, if the client and server's replay cache supports 5 DSI
requests, if the client sends 5 requests with DSI request IDs of 1, 2,
3, 4, and 5, the AFP Server caches replies for requests 1, 2, 3, 4, and
5. When the next DSI request is sent by the AFP client, it has a DSI
Request ID of 6. On the AFP server, when the request with ID 6 arrives,
the server knows that the reply for DSI request ID 1 was successfully
received by the AFP client. Thus, the reply for the request with ID 1
can now be freed. When the request with ID 7 is received by the AFP
server, it frees the reply for the request with ID 2. The client will
never send more requests than the maximum number of requests in the
replay cache.

It is recommended that the replay cache be large enough to hold at least
32 requests, but strictly less than 65,536.

If the server includes a `kServerReplayCacheSize` option in the data
portion of the `DSIOpenSession` reply packet, then it is assumed that
the server supports the replay cache. If the replay cache is supported
by the server, the client does not reset the *Request ID* field to zero
in the DSI header on reconnect. This persistent request ID allows the
server to detect whether a request is a replayed request or a new
request from the client.

The AFP server keeps a replay cache containing replies that it has sent.
When a request arrives from the client, the server searches this cache
looking for a matching DSI request ID. If a matching ID is found, the
server compares the AFP command byte with the original request to make
sure that they match. If the DSI request ID and AFP command byte match,
the AFP Server sends the reply from the replay cache. If a match is not
found in the cache, then the AFP Server should process it as a new
request from the client.

With a replay AFP client, the DS request IDs are persistent which means
they must not be reused unless the request is a replay of a previous
request (meaning that the client never got the original reply, so it
replays the request after a successful primary reconnect) or the ID has
wrapped around back to that same number.

All AFP commands can be cached in the Replay cache if you want, but only
a subset of the AFP commands are non-idempotent and must be cached.
These commands are:

- FPByteRangeLock

- FPByteRangeLockExt

- FPChangePassword

- FPCloseFork

- FPCloseVol

- FPCopyFile

- FPCreateDir

- FPCreateFile

- FPDelete

- FPExchangeFiles

- FPFlush

- FPFlushFork

- FPRemoveExtendedAttr

- FPMoveAndRename

- FPOpenFork

- FPOpenVol

- FPRename

- FPSetDirParms

- FPSetFileDirParms

- FPSetFileParms

- FPSetForkParms

- FPSetVolParms

- FPSetExtendedAttr

- FPSetACL

- FPLink

- FPSyncDir

- FPSyncFork

The replay cache is useful *only* if a Primary Reconnect is successful.
If primary reconnect fails, then the replay cache was not found, and
replay is not possible. In this case, any pending requests on the client
in its replay cache are discarded and resent as new requests.

When the AFP client gets disconnected, it puts any still-outstanding
requests on hold. After a successful primary reconnect, it replays those
requests exactly as they had been sent out before.

DSI headers for AFP/TCP are described in [AFP Over TCP](../afp_over_tcp).

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/AFPReplayCache/AFPReplayCache.html)
and presented here strictly for archival purposes.
