---
title: "AFP Character Encoding"
date: 2012-12-13
draft: false
type: "programming_guide"
weight: 12
---

# AFP Character Encoding

If the server and the sharepoint support UTF-8 names, the AFP server and
client send and receive decomposed UTF-8. However, characters in the
range of U2000 to U2FFF, UFE30 to UFE4F, and U2F800 to U2FA1F are not
decomposed. For complex characters, Unicode 3.2-based tables are used.
For additional information, see [http://developer.apple.com/technotes/tn/tn1150.html#UnicodeSubtleties](https://web.archive.org/web/20100722031935/http://developer.apple.com/mac/library/technotes/tn/tn1150.html#UnicodeSubtleties)
and the Unicode specifications.

For Macintosh Roman, AFP utilizes character string entity names that can
be composed of any 8-bit character. Character representations are
exactly the same as those used by the Mac OS and are shown in
Figure 2-1.

**Note:** The information in this section applies only to Macintosh
Roman character representations and does not apply to Unicode character
representations.

![AFP character set mapping](/images_character_encoding/afp_l_07_2x.png)
**Figure 2-1**  AFP character set mapping

Throughout AFP, character string comparison is done in a
case-insensitive manner (that is, K = k) except when a case-sensitive
volume is mounted. String comparison must also be done in a
diacritical-sensitive manner (for example, e is not equal to é).

Technical Note TN1150: *[HFS Plus Volume Format](https://web.archive.org/web/20100722031935/http://developer.apple.com/mac/library/technotes/tn/tn1150.html)*
describes the rules for uppercase equivalence of characters in AFP. Note
that this mapping does not exactly conform to the standards used in all
human languages. In certain languages (French, for example), the
uppercase equivalent of é is E; in other languages (and in AFP), the
uppercase equivalent of é is É.

----

Copyright © 2012 Apple Inc. All Rights Reserved. | Updated: 2012-12-13

**DISCLAIMER:** This website is not affiliated with Apple Inc. in any way.
The information in this section is a mirror of the content published at
[Apple Developer](https://developer.apple.com/library/archive/documentation/Networking/Conceptual/AFP/CharacterEncoding/CharacterEncoding.html)
and presented here strictly for archival purposes.
