---
title: "Using Directory Commands"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 20
---

# Using Directory Commands

AFP provides these commands for working on directories:

- `FPSetDirParms`

- `FPOpenDir` (deprecated)

- `FPCloseDir` (deprecated)

- `FPEnumerate`, `FPEnumerateExt`, and `FPEnumerateExt2`

- `FPCreateDir`

The `FPSetDirParms` command allows the AFP client to modify a
directory’s parameters. To obtain a directory’s parameters from the file
server, the AFP client uses the `FPGetFileDirParms` command, which is
described in the section [Using Combined Directory and File Commands](../combined_directory_and_file_commands).

On variable Directory ID volumes, the AFP client uses the `FPOpenDir`
command to open a directory on and retrieve its Directory ID. The
Directory ID is used in subsequent commands to enumerate the directory
or to obtain access to its offspring. For variable Directory ID volumes,
the `FPOpenDir` command is the only way to retrieve the Directory ID.
Calling `FPGetFileDirParms`, `FPEnumerate`, `FPEnumerateExt, `or
`FPEnumerateExt2` to retrieve the Directory ID on such volumes causes an
error to be returned.

On a fixed Directory ID volume, calling `FPGetFileDirParms`,
`FPEnumerate`, `FPEnumerateExt`, or `FPEnumerateExt2` is the preferred
way to obtain a Directory ID, although calling `FPOpenDir` also works.

The AFP client can close directories on variable Directory ID volumes by
sending the `FPCloseDir` command, which invalidates the corresponding
Directory ID.

The AFP client uses the `FPEnumerate`, `FPEnumerateExt`, and
`FPEnumerateExt2` commands to list, or enumerate, the files and
directories contained within a specified directory. In reply to this
command, the server returns a list of directory or file parameters
corresponding to those offspring. The `FPEnumerateExt` command differs
from the `FPEnumerate `command in that the `FPEnumerateExt` command is
prepared to handle larger values that may be returned when volumes are
larger than 4 GB in size. The `FPEnumerateExt2` command differs from the
`FPEnumerate` command in that the `StartIndex` and `MaxReplySize`
components to the `FPEnumerateExt2` command are longs, allowing you to
specify larger values than can be specified by the `FPEnumerate` and
`FPEnumerateExt` commands.

Directories are created by the `FPCreateDir` command.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/UsingDirectoryCommands/UsingDirectoryCommands.html)
and presented here strictly for archival purposes.
