---
title: postgresql user
---

## hints

* after installed, you can access the server using ``postgres`` account as **superuser**
  * from localhost
  * login as ``postgres`` or use ``-U postgres`` (as root) from **localhost**, no password is required
* there's no **default** password 
* jdbc connection string
  * ``jdbc:postgresql:<host[:port]>/<database>?user=<USER>&password=<PASSWD>``
  * non-alphabet character should be url-encoded, such as ``-`` to ``%2D``


## create a user

* login as ``postgres``
* run command
  ```bash
  createuser name
  ```
* TBC
