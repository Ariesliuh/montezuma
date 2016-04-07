# Montezuma #

Montezuma is a full-text indexing/search engine library written entirely in Common Lisp.

Montezuma is a Common Lisp port of [Ferret](http://ferret.davebalmain.com/trac).  Ferret is a Ruby port of [Lucene](http://lucene.apache.org/).  Lucene is sort of [Doug Cutting](http://nutch.sourceforge.net/blog/cutting.html)'s Java version of Text Database (TDB), which he and Jan Pedersen developed at Xerox PARC, and which, to complete the circle, was written in Common Lisp (see "[An Object-Oriented Architecture for Text Retrieval](http://lucene.sourceforge.net/papers/riao91.ps)").

We are hoping Montezuma will have better performance than both Ferret and Lucene, not because of doing anything fancy, but because of relying on native code-generating Common Lisp implementations.  Currently performance approaches that of Lucene, but is far from Ferret's relatively blazing speed.  See PerformanceComparisons.

Montezuma is named after the [Montezuma Oropendola](http://en.wikipedia.org/wiki/Montezuma_Oropendola).

## Current Status ##

Montezuma is reasonably stable software that has been used in a couple of production-level projects.

The first release was made July 13, 2006. Version 1.0 was tagged on 24 Feb 2012.

To install and load it using Quicklisp:

```
(ql:quickload :montezuma)
```

You can also download a tarball or check out the latest source via [Github](http://www.github.com/).

Indexing is complete, with both in-memory indices and indices on disk.

Single-term queries, boolean queries, phrase queries and wildcard queries basically work (though there are [report:1 bugs]).  Queries can be constructed via the API as well as by parsing a simple query language.

## Requirements ##

Montezuma uses [CL-PPCRE](http://www.weitz.de/cl-ppcre/) and [CL-FAD](http://www.weitz.de/cl-fad/), both of which are ASDF-installable.

## Loading, Running, Testing ##

Load via ASDF:

```
CL-USER> (asdf:oos 'asdf:load-op '#:montezuma)
; loading system definition from
; /Users/wiseman/src/montezuma/montezuma.asd into #<PACKAGE "ASDF4465">
; registering #<SYSTEM #:MONTEZUMA {106891F1}> as MONTEZUMA
; registering #<SYSTEM #:MONTEZUMA-TESTS {10A489A1}> as MONTEZUMA-TESTS
; ...
```

Load and run unit tests via ASDF:

```
CL-USER> (asdf:oos 'asdf:test-op '#:montezuma)

; compiling file "/Users/wiseman/src/montezuma/tests/unit/tests.lisp" (written 23 FEB 2006 11:37:38 AM):
; ...
;; MONTEZUMA::TEST-PRIORITY-QUEUE ................
;; MONTEZUMA::TEST-PRIORITY-QUEUE-CLEAR ..
;; MONTEZUMA::TEST-PRIORITY-QUEUE-STRESS .
;; MONTEZUMA::TEST-RAM-STORE .............................................................................
;; MONTEZUMA::TEST-FS-STORE .............................................................................
;; MONTEZUMA::TEST-STANDARD-FIELD ...........
; ...
```

Run individual tests (or test fixtures):

```
CL-USER> (montezuma::run-test-named 'montezuma::test-segment-info)
;; MONTEZUMA::TEST-SEGMENT-INFO ......
```

## Development Strategy ##

1. Make an initial hack & slash port of Ferret to Lisp.  This is basically a transliteration of the Ruby code to Lisp.  It might be ugly, it might not be idiomatic, but the goal is to get something working quickly.  Unit tests will be ported as well.  Some features may be left unimplemented (e.g., thread- and process-level locking).

2. Clean it up.  Turn it into code that Lispers will enjoy.  Craft a nice external API and let it out.  A comprehensive library of unit tests will be critical to avoid breakage.

3. Tune performance and finish out the feature list.  Once the code reaches a point where it is both adequately useful and adequately pretty, begin the process of attacking the the last 20%, which is a task that will presumably never be complete.  Add benchmark tests, fix bugs, etc.  Ideally I will find someone who thinks this is fun--and dump the project on them.

We're somewhere between (2) and (3) now.

## Mailing list/Discussion Group ##

There is a [Montezuma discussion group/mailing list](http://groups.google.com/group/montezuma-dev) for users and developers alike.