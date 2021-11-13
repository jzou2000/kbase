---
title: Changes and change
nav: changes/change
---

## list changes

```bash
p4 change -c client -s pending
```

## change - create, edit, delete

* create
  ```sh
  p4 change
  ```
* edit
  ```sh
  p4 change 12345
  ```
* delete
  ```sh
  p4 change -d 12345
  ```
  no file should be opened in the CL.
  Use following command to rever open files.
  ```sh
  p4 revert -c 12345 //SimbaTestTools/stk/Trunk/mk/...
  ```
  revert all files in //SimbaTestTools/stk/Trunk/mk/ of CL12345
* other flags
  * -o write to stdout
  * -i input from stdin
  *


## unshelve

```sh
p4 unshelve -s 12345
```
