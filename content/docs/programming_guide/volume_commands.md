---
title: "Using Volume Commands"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 19
---

# Using Volume Commands

AFP provides the following volume-level commands:

- `FPOpenVol`

- `FPCloseVol`

- `FPGetVolParms`

- `FPSetVolParms`

- `FPFlush`

- `FPCatSearch` and `FPCatSearchExt`

After obtaining the volume names through the `FPGetSrvrParms` command,
the AFP client sends an `FPOpenVol` command for each volume to which it
wants to gain access. If a volume has a password, it must be supplied at
this time. The command returns the requested volume parameters,
including the volume identifier, *VolumeID*.

The volume identifier is used in all subsequent commands to identify the
volume for which the commands apply and remains valid until the session
is terminated by calling `FPLogout` or the volume is closed by calling
`FPVolClose`.

After obtaining the volume’s volume identifier, the AFP client can
obtain the volume’s parameters by calling `FPGetVolParms`. The AFP
client can also change the volume’s parameters by calling
`FPSetVolParms`.

The `FPFlush` command requests that the server flush (write to disk) any
data associated with a particular volume.

The `FPCatSearch` and `FPCatSearchExt` commands search a volume for
files that match specified criteria. The `FPCatSearchExt` command
differs from the `FPCatSearch` command in that `FPCatSearchExt` is
prepared to handle the larger values that may be returned for searches
on volumes greater than 4 GB in size.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/UsingVolumeCommands/UsingVolumeCommands.html)
and presented here strictly for archival purposes.
