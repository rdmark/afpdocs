---
title: "AFP Version Differences"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 25
---

# AFP Version Differences

This document as a whole describes the current version of the Apple
Filing Protocol. This section provides a list of what commands were
added in each AFP version.

For a complete description of the commands themselves, see *Apple Filing
Protocol Reference*.

## Missing AFP Command Codes

12 and 13 were missing from Inside AppleTalk and have never been
allocated.

38-43 were missing from Inside AppleTalk but were added in AFP 2.1;
presumably they were preallocated for System 7.0.

44-47 and 50 were missing from Inside AppleTalk and have never been
allocated.

76 was added in AFP 3.2+, but will not be documented.

77 was used in prerelease versions of AFP 3.2+ but was discontinued
before GM.

## AFP 2.0

This version of the protocol is the version that was initially
documented in *Inside AppleTalk*. The contents of *Inside AppleTalk* are
now split between this document and *Apple Filing Protocol Reference*.

## AFP 2.1

This version was a significant upgrade to accommodate System 7.0.

- Added two way random number exchange UAM

- Added the notion of blank access privileges

- User and group IDs are now interchangeable

- Added `FPGetSrvrMsg` (AFP command 38)

- Added `FPCreateID` (AFP command 39)

- Added `FPDeleteID` (AFP command 40)

- Added `FPResolveID` (AFP command 41)

- Added `FPExchangeFiles` (AFP command 42)

- Added `FPCatSearch` (AFP command 43)

- Added `kAttrIsExpFolder` and `kAttrInExpFolder` flags (0x0002 and
  0x0010) returned by `FPGetFileDirParms`

- Added `kAttrMounted` flag (0x0008) returned by `FPGetFileDirParms`

- Added `kDontAllowSavePwd` bit (0x0004) to Flags returned by
  `FPGetSrvrInfo`

- Added `kSupportsSrvrMsg` bit (0x0008) to Flags returned by
  `FPGetSrvrInfo`

- Added `kHasVolumePassword` bit (0x0002) to `Volume Attributes Bitmap`

- Added `kSupportsFileIDs` bit (0x0004) to `Volume Attributes Bitmap`

- Added `kSupportsCatSearch` bit (0x0008) to `Volume Attributes Bitmap`

- Added `kSupportsBlankAccessPrivs` bit (0x0010) to
  `Volume Attributes Bitmap` returned by `FPGetVolParms`.

- Added `kFPIDNotFound` (-5034) error code

- Added `kFPIDExists` (-5035) error code

- Added `kFPDiffVolErr` (-5036) error code

- Added `kFPCatalogChanged` (-5037) error code

- Added `kFPSameObjectErr` (-5038) error code

- Added `kFPBadIDErr` (-5039) error code

- Added `kFPPwdSameErr` (-5040) error code

- Added `kFPPwdTooShortErr` (-5041) error code

- Added `kFPPwdExpiredErr` (-5042) error code

- Added `kFPInsideSharedErr` (-5043) error code

- Added `kFPInsideTrashErr` (-5044) error code

## AFP 2.2

- Added support for AFP over TCP.

- Added `kSrvrSig` bit (0x0010) to Flags returned by `FPGetSrvrInfo`.

- Added `kSupportsTCP` bit (0x0020) to Flags returned by
  `FPGetSrvrInfo`.

- Added `kSupportsSrvrNotify` bit (0x0040) to Flags returned by
  `FPGetSrvrInfo`.

- Added `kFPVolExtBytesFreeBit` (0x0200) to `Volume Bitmap`.

- Added `kFPVolExtBytesTotalBit` (0x0400) to `Volume Bitmap`.

- Added `kFPVolBlockSizeBit` (0x0800) to `Volume Bitmap`.

- The `FPOpenVol` command now uses the same bitmap as the
  `FPGetVolParms` command.

- Added attention mechanism.

- Added `kFPPwdNeedsChangeErr` (-5045) error code.

## AFP 3.0

Introduced in OS X v.10.0 and also used in v.10.1, AFP 3.0 includes
major changes to support OS X.

- Support for UTF-8 names almost everywhere.

- Support for files of 2 GB or more.

- Support for UNIX privileges.

- Support for reconnect.

- Support for Open Directory-based servers.

- Added "DHCAST128" UAM, later backported to classic Mac OS.

- Added `kFPUTF8Name` (3) path type

- Added subfunction `kUserIDToUTF8Name` (3) to FPMapID

- Added subfunction `kGroupIDToUTF8Name` (4) to FPMapID

- Added subfunction `kUTF8NameToUserID` (1) to FPMapName

- Added subfunction `kUTF8NameToGroupID` (2) to FPMapName

- Added `kUTF8SrvrMsg` (0x0002) to the MessageBitmap in `FPGetSrvrMsg`

- Changed meaning of 0x2000 in `File Bitmap` from `kFPProDOSInfoBit` to
  `kFPUTF8NameBit`

- Added `kFPUnixPrivsBit` (0x8000) to `File Bitmap`

- Added `FPReadExt` (AFP command 60)

- Added `FPWriteExt` (AFP command 61)

- Added `FPEnumerateExt` (AFP command 66)

- Added `FPByteRangeLockExt` (AFP command 59)

- Added `FPCatSearchExt` (AFP command 67)

- Added `FPGetAuthMethods` (AFP command 62)

- Added `FPLoginExt` (AFP command 63)

- Added `FPGetSessionToken` (AFP command 64)

- Added `kLoginWithID` (1) session token type

- Added `FPDisconnectOldSession` (AFP command 65)

- Added `kSupportsReconnect` bit (0x0080) to Flags returned by
  `FPGetSrvrInfo`

- Added `kSupportsDirServices` bit (0x0100) to Flags returned by
  `FPGetSrvrInfo`

- Added `kFPPwdPolicyErr` (-5046) error code

## AFP 3.1

Introduced in OS X v.10.2, AFP 3.1 was a relatively minor release to tidy
up some nagging OS X issues.

- Added "DHX2" UAM

- Added "Client Krb v2" UAM

- Added `kFPDiskQuotaExceeded` (-5047) error code

- Added `FPEnumerateExt2` (AFP command 68)

- Added `kNoNetworkUserIDs` (0x80) to `Volume Attributes Bitmap`.

- Added `kReconnWithID` (2) session token type

- Added `kLoginWithTimeAndID` (3) session token type

- Added `kReconnWithTimeAndID` (4) session token type

## AFP 3.1+

Introduced in OS X v.10.3, AFP 3.1+ added additional reconnection
functionality and additional Kerberos support.

- Added "Recon1" UAM.

- Added `kDefaultPrivsFromParent` (0x100) to `Volume Attributes Bitmap`

- Added `kRecon1Login` (5) session token type

- Added `kRecon1ReconnectLogin` (6) session token type

- Added `kRecon1RefreshToken` (7) session token type

- Added `kGetKerberosSessionKey` (8) session token type

## AFP 3.2

Introduced in OS X v.10.4, AFP 3.2 added support for ACLs and extended
attributes.

- Added `FPGetExtAttr` (AFP command 69)

- Added `FPSetExtAttr` (AFP command 70)

- Added `FPRemoveExtAttr` (AFP command 71)

- Added `FPListExtAttrs` (AFP command 72)

- Added `FPGetACL` (AFP command 73)

- Added `FPSetACL` (AFP command 74)

- Added `FPAccess` (AFP command 75)

- Added `kSupportsUTF8SrvrName` (0x200) to `Server Flags Bitmap`

- Added `kSupportsUUIDs` (0x400) to `Server Flags Bitmap`

- Added `kNoExchangeFiles` (0x200) to `Volume Attributes Bitmap`

- Added `kSupportsExtAttrs` (0x400) to `Volume Attributes Bitmap`

- Added `kSupportsACLs` (0x800) to `Volume Attributes Bitmap`

- Added subfunction `kUserUUIDToUTF8Name` (5) to `FPMapID`

- Added subfunction `kGroupUUIDToUTF8Name` (6) to `FPMapID`

- Added subfunction `kUTF8NameToUserUUID` (5) to `FPMapName`

- Added subfunction `kUTF8NameToGroupUUID` (6) to `FPMapName`

## AFP 3.2+

Introduced in OS X v.10.5, AFP 3.2+ added better synchronization support
for Time Machine.

- Added `FPSpotlightRPC` (AFP command 76) for private Apple use

- Added `FPSyncDir` (AFP command 78)

- Added `FPSyncFork` (AFP command 79)

- Added `kSupportsExtSleep` (0x800) to `Server Flags Bitmap`

- Added `kCaseSensitive` (0x1000) to `Volume Attributes Bitmap`

## AFP 3.3

Introduced in OS X v.10.6. Mandates support for the AFP replay cache
(described in [AFP Replay Cache](../replay_cache)).

## AFP 3.4

Introduced in OS X v.10.8. Changes the error code mapping so that the
POSIX error code `ENOATTR` maps onto the `kFPItemNotFound` AFP error
code. (In previous versions, an `ENOATTR` on the server side produced a
`kFPMiscErr` AFP error code.)

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/AFPVersionDifferences/AFPVersionDifferences.html)
and presented here strictly for archival purposes.
