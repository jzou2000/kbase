---
title: My docker that runs hugo
date: 2019-11-21
nav: my hugo docker
tags: [docker, setup, tips]
weight: 30
---

## Setup

## Run

By default the script runhugo

1. accept a list of folder as toplevel content section
1. clean target folder
1. generate the site and *watch* the input folder to updte

Example

```bash
runhugo
```

Note:

* the default topleve list is ``kbase simba books bookmarks``


To run interactively

```bash
runhugo -i  kbase simba books bookmarks
hugo -w --cleanDestinationDir

# alternately you can specified config and themem
# runhugo -i -c config-my.yaml -t ~/tmp/ssg kbase simba
# hugo -w -t mytheme --cleanDestinationDir


```

## Theme


