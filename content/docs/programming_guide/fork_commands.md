---
title: "Using Fork Commands"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 23
---

# Using Fork Commands

AFP provides these fork-level commands:

- `FPGetForkParms`

- `FPSetForkParms`

- `FPOpenFork`

- `FPRead` and `FPReadExt`

- `FPWrite` and `FPWriteExt`

- `FPFlushFork`

- `FPByteRangeLock` and `FPByteRangeLockExt`

- `FPCloseFork`

The AFP client uses the `FPGetForkParms` command to read a fork’s
parameters.

The `FPSetForkParms` command is used to modify a fork’s parameters.

The `FPOpenFork` command is used to open either fork of an existing
file. This command returns an open fork reference number, which is used
in subsequent commands for this open fork.

The `FPRead` and `FPReadExt` commands are used to read the contents of
the fork. The `FPReadExt` command differs from the `FPRead` command in
that the `FPReadExt` command is prepared to handle large values that may
be returned for volumes greater than 4 GB in size.

The `FPWrite` and `FPWriteExt` commands are used to write to a fork. The
`FPWriteExt` command differs from the `FPWrite` command in that the
`FPWriteExt` command is prepared to handle the large values that are
required for writing to volumes greater than 4 GB in size.

The `FPFlushFork` command is used to request that server write to disk
any of the fork’s data that is in the server’s internal buffers.

The `FPByteRangeLock` and `FPByteRangeLockExt` commands are used to lock
ranges of bytes in the fork. The `FPByteRangeLockExt` command differs
from the `FPByteRangeLock` command in that the `FPByteRangeLockExt`
command is prepared to handle large values that are required for locking
ranges on volumes greater than 4 GB in size. Locks allow multiple users
to share a file’s open fork. Locking a range of bytes prevents other AFP
clients from reading or writing data within the specified range. If an
AFP client locks a byte range, that range is reserved for exclusive
manipulation by the client that placed the lock.

The `FPCloseFork` command is used to close an open fork. This command
invalidates the open fork reference number that was assigned when the
fork was opened.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/UsingForkCommands/UsingForkCommands.html)
and presented here strictly for archival purposes.
