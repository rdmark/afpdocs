---
title: "Using File Commands"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 21
---

# Using File Commands

AFP provides these commands for working on files:

- `FPSetFileDirParms`

- `FPCreateFile`

- `FPCopyFile`

- `FPCreateID` (deprecated)

- `FPDeleteID` (deprecated)

- `FPResolveID`

- `FPExchangeFiles`

The AFP client uses the `FPSetFileParms` command to modify a specified
file’s parameters, the `FPCreateFile` command to create a file, and the
`FPCopyFile` command to copy a file that exists on a volume managed by a
server to any other volume managed by that server. To obtain a specified
file’s parameters, the AFP client uses the `FPGetFileDirParms` command,
discussed in the next section.

The `FPCreateID` command creates a unique File ID for an existing file,
and `FPDeleteID` removes a File ID.

The `FPResolveID` command uses a File ID to retrieve information about a
file.

The `FPExchangeFiles` command preserves existing file IDs when an
application performs a Save or a Save As operation.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/UsingFileCommands/UsingFileCommands.html)
and presented here strictly for archival purposes.
