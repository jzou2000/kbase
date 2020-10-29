---
title: WSL 2 tips
---

# WSL 2 Features

# Install WSL 2

# WSL GUI

## VcXsrv

VcXsrv is an open source X server on Windows, with GPL license.

Note:
* allow it access Windows Firewall, use either of these solutions
  * enable access from private/domain/public at the first time launch, or
  * change it through following path in Windows Settings
    *  Update & Security
    *  Windows Security
    *  Firewall & network protection
    *  Allow an app through firewall
    *  find VcXsrv in "allowed apps and features" list, and enable all of Domain/Private/Public
 * can we disable firewall for all WSL?

## Set DISPLAY in WSL

Because WSL is a virtual machine inside the Windows host, we can't access the X server that runs on Windows host as ``localhost``.


```bash

```
