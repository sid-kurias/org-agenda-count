# org-agenda-count
This module provides functionality for counting the number of entries
in a custom agenda block, and displaying that count in the agenda.  

This repository is just a sync of the code written by
[Aaron Harris](https://bitbucket.org/apharris/). The original URL
is in a [Bitbucket Repository](https://bitbucket.org/apharris/emacs-init/src/)

This module provides functionality for counting the number of
 entries in a custom agenda block, and displaying that count in the
 agenda.

 To use it, define a custom agenda command in the usual way, and set
 the variable `org-agenda-overriding-header` to a value that
 incorporates the return value of the function `org-agenda-count`.
 You can think of this function as returning a string containing the
 number of entries in that agenda block, but the function actually
 returns a proxy string and sets up its eventual replacement with
 the correct value; this is necessary because of the way various
 parts of the agenda are constructed.

 The `org-agenda-count` function takes an optional argument (a
 string) that identifies the block it appears in.  If multiple
 blocks in a single agenda are being counted, all of them need
 distinct identifiers; if only one block is being counted, its
 identifier can be omitted.

 A typical use case is as follows:

``` emacs-lisp
((agenda
    ""
    ((org-agenda-overriding-header
      (format "Foo [%s]" (org-agenda-count "foo")))))
   (tags-todo
    "bar"
    ((org-agenda-overriding-header
      (format "Bar [%s]" (org-agenda-count "bar")))
     (org-agenda-max-entries 5))))

```
 This will associate counts with both blocks, but notice that the
 "Bar" block sets `org-agenda-max-entries'.  Its count will not
 display 5, but rather the number of entries that would be displayed
 without this limitation.

 By default, the proxy value that `org-agenda-count` uses is of the
 form "##<block>##", where "<block>" stands for the supplied block
 identifier.  If the double hashes cause trouble for you, this can
 be changed with the option `org-agenda-count-delimiter'.  Whatever
 the value of this option, it should not appear as a substring of
 your block identifiers.
