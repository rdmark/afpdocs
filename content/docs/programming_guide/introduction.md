---
title: "Introduction"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 10
---

# Introduction

The Apple Filing Protocol (AFP) allows users of multiple computers to
share files easily and efficiently over a network.

This document describes the AFP wire protocol at a conceptual level. For
detailed information about the request blocks that an AFP client sends
to an AFP server and the reply blocks that an AFP server sends to an AFP
client in response to a request block, see *Apple Filing Protocol
Reference*.

Note that all values exchanged between an AFP client and an AFP server
are sent over the network in network byte order.

## Organization of This Document

This book contains the following chapters:

- Apple Filing Protocol Concepts
  describes the concepts used in the AFP architecture.

- Using Login Commands describes
  the commands used to open and close a connection with a file server.

- Using Volume Commands describes
  the commands for interacting with a file server volume.

- Using Directory Commands
  describes the commands for using directories.

- Using File Commands describes the
  commands for working on files.

- Using Combined Directory and File Commands
  describes commands that can be used on both files and directories.

- Using Fork Commands describes the
  commands to interact with data forks.

- Using Desktop Database Commands
  describes the commands to read and write information store in the
  server's desktop database.

## See Also

Refer to the following reference document for AFP:

- *Apple Filing Protocol Reference*

The following sources provide additional information that may be of
interested to AFP developers:

- *Inside AppleTalk*. Addison Wesley. ISBN 0-201-19257-8.

- *Applied Cryptography, Second Edition*, by Bruce Schneier.
  Specifically, the chapter on Diffie-Hellman Key Exchange.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/Introduction/Introduction.html)
and presented here strictly for archival purposes.
