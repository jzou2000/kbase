---
title: Package a node.js application into a single binary
date: 2019-02-27
tags: pkg package node.js binary
---

# install
````bash
npm install pkg -g
pkg --help
````

# usage

````bash

cd project
pkg -o output-file -t ${nodev}-linux,${nodev}-win entry.js
````

# using assets

