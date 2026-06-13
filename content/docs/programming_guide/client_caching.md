---
title: "AFP Client Caching"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 18
---

# AFP Client Caching

This chapter describes how the AFP client in OS X v.10.2 and later caches
data before sending it to an AFP server.

First, some terms and definitions:

- Universal Buffer Cache (UBC)—A page cache that includes file data
  caching, memory-mapped I/O backing, and so on. The buffer cache is
  said to be unified because it exists as part of the normal virtual
  memory physical page pool rather than as a separately managed buffer.

- Dirty file data—Data that has been changed in the UBC but that has not
  yet been written out to permanent storage (to the disk or file
  server).

- Cache consistency—Consistency between the client’s data in the UBC and
  the data on the server.

- `ubc_clean`— A routine that pushes out to storage any dirty file data
  in virtual memory and that releases any buffers in the UBC associated
  with valid clean pages. Optionally, the pages in virtual memory may be
  discarded.

- Cluster routines—`cluster_read`, `cluster_write`, etc. These routines
  group small read and write calls into larger, page-aligned read and
  write calls that take advantage of the UBC. If the requested data is
  already in the UBC, the call is completed using the local data.

## File Data Caching

By default, the AFP client uses the UBC to cache file data, with the
following exceptions:

- Files for which byte range locks are set

- Files that are symbolic links

The AFP client checks cache consistency during the following operations:

- Opens —When an AFP client closes a file on the server, it saves the
  file’s last modification date. The next time the client opens the
  file, it compares the file’s current last modification date with the
  last modification date the client saved. If the dates do not match,
  the client assumes that another client has modified the file and calls
  `ubc_clean` to discard the current cached data.

- Reads and writes—The AFP client is implemented in part as a Virtual
  File System and thus can be called by user processes as well as kernel
  processes. Kernel processes can make read and write calls without
  first making an open. When called by a kernel process, the client
  makes an open call before doing the read or write operation. Before
  the open call is made, the client compares the file’s current
  modification date on the server with the client’s saved modification
  date. If the dates do not match, the client assumes that another
  client has modified the file and calls `ubc_clean` to discard the
  current cached data.

- Attempts to access a file on the server after the server has sent a
  Volume Change Attention packet when DenyWrite is not set for the
  file—The file’s current modification date on the server is compared
  with the client’s saved modification date. If the server’s current
  modification data differs from the client’s saved modification date,
  the client calls `ubc_clean` to discard the current cached data. If
  the server does not support the Volume Change Attention packet, the
  AFP client should poll the server at a maximum interval of ten seconds
  to check for changes.

</div>

## File Metadata Caching

Each file’s metadata is maintained in a vnode structure for that file.
The AFP client should check a file’s metadata for coherency with the
server when the AFP client accesses a vnode after the server has sent a
Volume Change Attention packet. Each vnode contains a time stamp of the
last Volume Change Attention packet that caused this vnode to be
updated. If the timestamp of the last received Volume Change Attention
is different from the timestamp in this vnode, this vnode’s file
metadata must be stale and the AFP client should send a request for the
latest information to the server.

Whenever an AFP client needs to use a file’s Modification date or fork
size information, it should ask the server for the current information.
To prevent the server from being flooded with requests, AFP clients
should limit their requests for metadata to one request per second.

In addition, file metadata in the AFP caches has a maximum Time To Live
(TTL) value. This TTL is intended to help when two clients have a file
open at the same time. Without this timer, if one client writes to the
file but never closes it, then a volume change attention packet would
never be sent by the server, so the second client would never see the
EOF change.

Because of the TTL timer, when the second client checks the EOF, if no
volume change attention packet has been received but the TTL timer has
expired, the client requests the latest information from the server
anyway. This is not really polling, per se, because it only occurs when
the vnode is accessed. If the vnode is never accessed, the TTL makes no
difference.

Recently modified files are assumed to be more likely to change than
files that have not changed in a while. For this reason, the TTL is
determined by taking the amount of time since the file was last
modified, dividing the value by 10, and limiting the minimum and maximum
values.

For example, with the default TTL values of 5 and 60 seconds:

- Metadata for a file modified less than 50 seconds ago has a TTL of 5
  seconds (the minimum TTL).

- Metadata for a file modified between 50 and 600 seconds (10 minutes)
  ago has a TTL of the time since last modification divided by 10 (in
  other words, 5–60 seconds).

- Metadata for a file modified more than 600 seconds (10 minutes) have a
  TTL of 60 seconds (the maximum TTL).

This algorithm is based on NFS metadata caching.

## Controlling Caching

There are two ways to disable data caching in the AFP client and access
the current data on the server:

Use the `noCacheMask` flag. See Technical note FL16 for more information
on how to use the `noCacheMask` flag.

Use the `fcntl` call on the file descriptor, as in the following
examples:

```c
(void) fcntl(fd, F_NOCACHE, 1); /* turn off data caching */
(void) fcntl(fd, F_NOCACHE, 0); /* turn on data caching */
```

Note that even though data caching in the AFP client may be disabled,
Carbon may still cache fork information like fork length and current
fork position.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/AFPClientCaching/AFPClientCaching.html)
and presented here strictly for archival purposes.
