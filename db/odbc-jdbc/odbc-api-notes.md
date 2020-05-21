---
title: ODBC API Notes
nav: odbc api notes
date: 2020-05-09
tags: [odbc, api, notes]
---

## Return Length

Most ODBC APIs that return length of string are in unit of bytes, except followings that are in unit of chars

|API       |Parameter  |Condition    |Descriptoin|
|:--------:|-----------|-------------|-------------|
|SQLGetInfo|StringLengthPtr|iodbc    | |