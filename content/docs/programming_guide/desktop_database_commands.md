---
title: "Using Desktop Database Commands"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 24
---

# Using Desktop Database Commands

**Note:** The Desktop database is no longer supported beginning in OS X
v.10.6.

An AFP client uses the following commands to read and write information
stored in the server’s Desktop database:

- `FPOpenDT`

- `FPCloseDT`

- `FPAddIcon`

- `FPGetIcon`

- `FPGetIconInfo`

- `FPAddAPPL`

- `FPRemoveAPPL`

- `FPGetAPPL`

- `FPAddComment`

- `FPRemoveComment`

- `FPGetComment`

Before any other Desktop database commands can be sent, the AFP client
must send an `FPOpenDT` command. This command returns a reference number
to be used in all subsequent commands on the Desktop database.

When access to the Desktop database is no longer needed, the AFP client
makes an `FPCloseDT` command.

`FPAddIcon` adds a new icon to the Desktop database, and `FPGetIcon`
retrieves the bitmap for a given icon as specified by its file creator
and type. `FPGetIconInfo` retrieves a description of an icon. This
command can be used to determine the set of icons associated with a
given application. Successive `FPGetIconInfo` commands return
information on all icons associated with a given file creator.

`FPAddAPPL` adds an APPL mapping for the specified application and its
file creator. `FPRemoveAPPL` removes the specified application from the
list of APPL mappings corresponding to its file creator. It is the AFP
client’s responsibility to add and remove APPL mappings for applications
that are added to or removed from the volume, respectively. For
applications that are moved or renamed, the AFP client should remove the
old APPL mapping before the operation and add a new APPL mapping with
the updated information after the operation has been completed
successfully.

`FPGetAPPL` returns the next APPL mapping in the Desktop database’s list
of applications that correspond to a given file creator.

`FPAddComment` stores a comment string associated with a particular file
or directory on the volume. When adding a comment for a file or
directory that already has an associated comment, the existing comment
is replaced.

`FPRemoveComment` removes the comment associated with a particular file
or directory. `FPGetComment` retrieves the comment associated with a
particular file or directory.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/UsingDesktopDatabaseCommands/UsingDesktopDatabaseCommands.html)
and presented here strictly for archival purposes.
