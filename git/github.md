---
title: github issues
nav: github
description: miscelleous tips for accessing github
---

## PAT - Personal Access Token

Github has disabled password to access through command-line utilities and API authentication.
Instead, PAT is used whenever password is required.
PAT is a program generated string which can be considered a strong version of password,
because it looks a random string, stronger than human-generated __string__ password.

Here is the steps to generate PAT:

* start from any github page
* click on the top-right icon that is used for logout/settings/...
* click menu sequence: Settings|Developer Settings|Personal access tokens
* click button "Generate new token"
* fill the form and generate a token
  * a note describe the purpose of the token
  * expire is **strongly** recommended
  * enable a list of scope (grants)
* the token is generated and displayed, **copy and save** it to some safe place. You won't see it in github again.

Usage: simply use PAT as password whenever password is required.
```sh
$ git clone https://github.com/username/repo.git
Username: your_username
Password: your_token
```
