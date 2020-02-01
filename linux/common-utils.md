---
title: Common Used Utilities
tags: [utils]
---

## find

|Option        |Usage|
|--------------|-----|
|-ctime +n     |find objects that are created n days (n* 24hours) ago|
|-regex pattern|the whole path matches the pattern|
|-name pattern |pattern for file|
|-path pattern |pattern for the whole path|
|-not          |not operation|
|-and          |and operation|

Example - get list of all source files, excluding

*   list only files (not directories)
*   skip *.[od]      compile output
*   skip *.flist     output of script
*   skip b/*         shadow build at b/
*   skip *.tar       

```bash
# get list of all source files:
find * -type f -not -name '*.[od]' -and -not -name '*.flist' -and -not -name '*.tar' -and -not -path 'b/*' > src.flist
tar cvf src.tar --files-from=src.flist

```
## grep

## tar

