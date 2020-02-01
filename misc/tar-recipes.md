---
title: Some Tar Recipes
nav: tar recipes
description: Some useful recipes for using tar
keywords: [tar, recipe]
---

Tar is often used to pack a group of files in a single package (and vice versa).

## Choose only a subset of files

Tar has options to exclude files by pattern, but not
to include files. However it has an option that picks
files from a file, which can be either predefined
static file (manually edit or whatever) or generate dynamice by some powerful file picker such as ``find``.

Following example tar all xml files in the current folder.

```bash
find * -name '*.xml' | tar cvf my.tar --files-from -
```

Note:

* ``find`` generates a list of files to stdout
* ``tar`` picks files from specified file ``-``, or stdin, which is piped from ``find``.
* related options
  ```bash
  -T, --files-from=FILE
      get names from FILE
  -X, --exclude-from=FILE
      exclude patterns listed in FILE
  ```

## find

|object|option|description|
|------|------|-----------|
|number|+n/-n/n |greater than/less than/equal to n, for all following number (size, time, etc)|
|size|-size n[kMG] |file size of n (k/M/G). Other unit can be b/block, c/bytes, w/two-bytes|
|type|-type c|d/directory, f/file, l/symbolic link, s/socket, p/pipe, b/block dev, c/char dev|
|regex|-regex pattern|regex match full path|
|time|-mmin n|modified n minutes ago. others are -amin (access), -cmin (create)|
||-mtime n|modified n*24 hours (n days) ago|
||-newer file|modified more recently than file. others: -anewer, -cnewer|

### control the output format
By default (-print), find only shows the matched file pathname, by using -printf, you can control more information.


```bash
# find files that have size greater than 10MB,
# show size in bytes, modified time, and full pathname each line
find . -size 10M -printf '%s %TD %Tr %p\n'
48384732 11/06/18 10:29:14 AM ./SQL/ResultSets/BIG_JOINS-SQL_QUERY-21.xml
75575695 11/06/18 10:29:16 AM ./SQL/ResultSets/BIG_JOINS-SQL_QUERY-22.xml
35501993 11/06/18 10:29:27 AM ./SQL/ResultSets/BIG_JOINS-SQL_QUERY-32.xml
23365728 11/06/18 10:29:28 AM ./SQL/ResultSets/BIG_JOINS-SQL_QUERY-34.xml
75658212 11/06/18 10:29:31 AM ./SQL/ResultSets/BIG_JOINS-SQL_QUERY-43.xml
75668456 11/06/18 10:29:33 AM ./SQL/ResultSets/BIG_JOINS-SQL_QUERY-44.xml
```

More (common) formats

|format|description|
|----|----|
|%a|last a/access, c/created, t/modified time, in format of ctime|
|%Tk|last A/access, C/created, T/modified time, k format: D=mm/dd/yy, r=hh:mm:ss|
|%f|file name only, leading path removed|
|%h|leading path|
|%k|disk space in 1K blocks|
|%p|file's full name|
|%s|size in bytes|


