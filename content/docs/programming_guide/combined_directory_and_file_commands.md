---
title: "Using Combined Directory and File Commands"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 22
---

# Using Combined Directory and File Commands

AFP provides five commands that operate on both files and directories:

- `FPGetFileDirParms`

- `FPSetFileDirParms`

- `FPRename`

- `FPDelete`

- `FPMoveAndRename`

The AFP client uses the `FPGetFileDirParms` command to retrieve the
parameters associated with a given file or directory. When it uses this
command, the AFP client does not need specify whether the CNode is a
file or directory; the file server indicates the CNode’s type in
response to this command.

The `FPSetFileDirParms` command is used to set the parameters of a file
or directory. When the AFP client uses this command, it need not specify
whether the object is a file or directory. This command allows the AFP
client to set only those parameters that are common to both types of
CNodes.

The `FPRename` command is used to rename files and directories.

The `FPDelete` command is used to delete a file or directory. A file can
be deleted only if it is not open; a directory can be deleted only if it
is empty.

The `FPMoveandRename` command is used to move a file or a directory from
one parent directory to another on the same volume. The moved CNode can
renamed at the same time.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/UsingCombinedDirectoryandFileCommands/UsingCombinedDirectoryandFileCommands.html)
and presented here strictly for archival purposes.
