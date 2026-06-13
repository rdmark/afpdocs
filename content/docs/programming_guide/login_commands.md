---
title: "Using Login Commands"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 15
---

# Using Login Commands

An AFP client uses the following commands to get information about a
file server and to open and close a session with it:

- `FPGetSrvrInfo`

- `FPGetAuthMethods` (deprecated)

- `FPLogin` and `FPLoginExt`

- `FPLoginCont`

- `FPGetSrvrParms`

- `FPGetSessionToken`

- `FPDisconnectOldSession`

- `FPLogout`

- `FPMapID`

- `FPMapName`

- `FPChangePassword`

- `FPGetUserInfo`

The AFP client sends the `FPGetSrvrInfo` command to obtain server
information. The `FPGetSrvrInfo` command returns server information
including the following server parameters: server name, machine type,
AFP version strings, UAM strings, volume icon and mask, a bitmap of
flags, and optionally, a list of available Open Directory names. For
descriptions of server parameters, see `FPGetSrvrInfo` in the Reference
section.

From the lists of AFP versions and UAMs that the server supports, the
AFP client selects the highest AFP version and the most secure UAM that
the AFP client supports. To establish a session with the file server,
the AFP client includes the strings for the selected AFP version and UAM
in an `FPLogin` or `FPLoginExt` command.

When calling `FPLoginExt`, the AFP client must specify the user name in
UTF-8 encoding and specify the Open Directory domain in which the user
can be found. (A user name specified in UTF-8 encoding is the same as a
AFPName file name, except that there is no text encoding hint.)

In response to the `FPLogin` or `FPLoginExt` command, the server
performs user authentication. Depending on the selected UAM, the entire
user authentication process can involve one or more `FPLoginCont`
commands to complete the authentication process with the server. A
session is established between the file server and the AFP client when
the authentication process completes successfully.

After a session is established, the AFP client must obtain a list of the
server’s volumes. To obtain the list, the AFP client makes an
`FPGetSrvrParms` command, which returns the number of volumes shared by
the server, the names of the volumes, and whether they are
password-protected.

The `FPGetSessionToken` command gets a reconnect token that the AFP
client may later use if the session is disconnected unintentionally. In
the case of an unintentional disconnection, the AFP client logs in again
using the same user and authentication information that it used to log
in previously, re-establishes the state of the connection, and sends an
`FPDisconnectOldSession` command that passes the reconnect token to the
server to tell it to release resources associated with the disconnected
session.

When the AFP client user no longer needs to communicate with the server,
the AFP client issues an `FPLogout` command to terminate the session.

The `FPMapID` and `FPMapName` commands are used for directory access
control. The `FPMapID` command obtains the user or group name
corresponding to a given User or Group ID. The `FPMapName` command
converts a user or group name to the corresponding User or Group ID.

The `FPChangePassword` command changes a user’s password.

The `FPGetUserInfo` command retrieves information about a user.

The `FPGetSrvrMsg` command retrieves log in and server messages from the
server.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/UsingLoginCommands/UsingLoginCommands.html)
and presented here strictly for archival purposes.
