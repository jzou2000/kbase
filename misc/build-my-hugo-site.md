---
title: Build My Hugo Site
date: 2019-12-10
categories: [hugo]
keywords: [build, hugo, theme, git]
---

## What I have already

On github, I have these repos, they have been modified locally

* kbase - my knowledgebase markdown source
* jzou2000.github.io - my static site

On my local workstation, I have

* hugo/alpine docker
* empty hugo site ``myhugo``
* theme ``van`` developped in above site ``myhugo``
* some scripts that run hugo to generate the site and express.js to serve it

## Push my theme to github

1. create a repo named ``van``. After the repo is created, github shows
   steps to pull or push.
   ```bash
   # create a new repositiory on the command line
   echo "# van" >> README.md
   git init
   git add README.md
   git commit -m "first commit"
   git remote add origin https://github.com/jzou2000/van.git
   git push -u origin master
   ```
   ```bash
   # push an existing repoistory from the command line
   git remote add origin https://github.com/jzou2000/van.git
   git push -u origin master
   ```
1. go to theme folder to create a local repo
   ```bash
   cd ~/ssg/myhugo/themes/van
   git init
   git add .
   git commit -m 'initial commit of van, my ssg hugo theme'
   ```
1. follow the push step to push local van repo to github
   ```bash
   git remote add origin https://github.com/jzou2000/van.git
   git push -u origin master
   ```

## Regular Publish Steps

1. commit and push markdown pages
   ```bash
   cd ~/myhub/kbase
   git add .
   git commit -m 'I have updted some content in md'
   git push
   ```
1. run hugo (via docker) to generate the site (html)
   ```bash
   runhugo -N -g kbase books bookmarks
   # the target folder will be
   # ~/myhub/jzou2000.github.io
   # -N   don't use docker name (there's another hugo docker for locaer webs)
   # -g   for github
   ```
1. push hugo output to github
   ```bash
   cd ~/myhub/jzou2000.github.io
   git add .
   git commit -m 'update the site'
   git push
   ```

## Use netlify

To be finished.
