---
title: BinUtils
date: 2019-06-21
tags: [binutils, bin, utils]
---

[sourceware.org](https://sourceware.org/binutils/docs/binutils/index.html#SEC_Contents)

|Name       |Description|
|-----------|-----------|
|ar         |Create, modify, and extract from archives|
|nm         |List symbols from object files|
|objcopy    |Copy and translate object files|
|objdump    |Display information from object files|
|ranlib     |Generate index to archive contents|
|size       |List section sizes and total size|
|strings    |List printable strings from files|
|strip      |Discard symbols|
|c++filt    |Filter to demangle encoded C++ symbols|
|cxxfilt    |MS-DOS name for c++filt|
|addr2line  |Convert addresses to file and line|
|windmc     |Generator for Windows message resources|
|windres    |Manipulate Windows resources|
|dlltool    |Create files needed to build and use DLLs|
|readelf    |Display the contents of ELF format files|
|elfedit    |Update ELF header and property of ELF files|


## grep tips

|Option|Description|
|------|-------------|
|-v    |invert - show lines that **DO NOT** match|
|-r\|-R|recursively|
|-E    |use extended RE, such as ``abc|def``. ``-P`` for perl style (if supported)|
|-i    |ignore case|

## find recipe

|type|arg|example|description|also|
|:---|:-------|:--------------|:------------------------------|:----|
|test|+n      |+5     |greater than n|-n (less), n (equal)|
|    |-amin n |-amin 5|accessed n minutes ago|-cmin (change),-mmin (modify)|
|    |-anewer ref|-anewer main.o|accessed after the modification of ref file|
|    |-atime n|-atime 2|accesed n*24 hours ago|-ctime,-mtime|
|    |-newer ref|      |inode status change is newer than ref modification|
|    |-name pattern|-name *.o|name (glob) pattern|-path
|    |-regex pattern|-regex '.*abc.'|name of RE pattern|
|    |-size n       |-size -5k|size of the file, support M/G/...|
|    |-type t |-type d|file type (f-file,d-dir,s-socket,...)|
|    |-perm -mode|-perm -g=w|check permission, all of perm|mode,/mode|
|    |-user name|-user jzou|owner is name|-uid n|
|action|-print|            |print the file name (default)|
|      |-delete|           |delete the file|
|      |-exec cmd|-exec rm {} \;|execute a command, pass file as {}|-ok cmd, ask|
|      |-printf fmt|-printf '%P %s\n'|similar to printf(3C)|-fprintf, -printf0|
|operator|()|\( -type f \) | group||
|        |! |! -amin 2|not|-not, -a, -and, -o, -or|
|misc|-maxdepth levels|-maxdepth 3|max depths in recursive, 0 for no-subfolders||





* simple
  ```bash
  jasonz@VANLWIN0056:~/pkg/mpir2-gcc44$ find . -type f
  ./release32/include/mpir.h
  ./release32/lib/libmpir.so.8.2.1
  ./release32/lib/libmpir.la
  ./release32/lib/libmpir.a
  ./release32/share/info/mpir.info-2
  ./release32/share/info/mpir.info-1
  ./release32/share/info/mpir.info
  ./release32/share/info/dir
  ./release64/include/mpir.h
  ./release64/lib/libmpir.so.8.2.1
  ./release64/lib/libmpir.la
  ./release64/lib/libmpir.a
  ./release64/share/info/mpir.info-2
  ./release64/share/info/mpir.info-1
  ./release64/share/info/mpir.info
  ./release64/share/info/dir  
  ```
* name filter, output format
  ```bash
  jasonz@VANLWIN0056:~/pkg/mpir2-gcc44$ find . -type f -name 'lib*' -printf '%-40P %5k %CD %Cr\n'
  release32/lib/libmpir.so.8.2.1             484 04/27/21 03:54:16 PM
  release32/lib/libmpir.la                     4 04/27/21 03:54:16 PM
  release32/lib/libmpir.a                    952 04/27/21 03:54:16 PM
  release64/lib/libmpir.so.8.2.1             724 04/27/21 03:45:42 PM
  release64/lib/libmpir.la                     4 04/27/21 03:45:42 PM
  release64/lib/libmpir.a                   1388 04/27/21 03:45:42 PM
  ```

common printf fields

|token|example|description|
|-----|-------|-----------|
|P    |%-40P  |file name start from find-root, width=40, left-align|
|k    |%5k    |file size in kilo, width=5|
|C    |%CD    |change time, with time fields|
|     |D      |month/date/year|
|     |r      |local time 12-hour|
|     |H      |H=hour, M=minute, S=second-with-fraction|
