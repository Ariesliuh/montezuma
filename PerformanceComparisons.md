## A Simple Performance Comparison ##

I've compared the indexing performance of Montezuma against that of Lucene and Ferret.  This is an extension of the work Dave Balmain did [comparing Ferret and Lucene](http://ferret.davebalmain.com/trac/wiki/FerretVsLucene), and  I used the same corpus ([Reuters 21578](http://www.daviddlewis.com/resources/testcollections/reuters21578/)) and his code for Lucene and Ferret.

The test is to index 19,043 Reuters articles using the simple whitespace-analyzer.  Term vectors and the documents themselves are not stored.

|                     | [0.1.1](Montezuma.md)|[0.1.2](Montezuma.md)|Lucene 2.0 | Ferret 0.10.13 |
|:--------------------|:---------------------|:--------------------|:----------|:---------------|
|documents/s          | 31.62                           | 41.74                            | 56.01       | 521.6              |


[[Image(PerformanceComparisons:montezuma-0.1.2-performance-comparison-s.png)]]


I used Red Hat Fedora Core 5 (FC5) running under VMWare in Windows XP to do the comparisons.  SBCL 0.9.18 was used for Montezuma.