---
title: Sqlite System Tables
date: 2019-05-28
tags: [sqlite, systable, system]
---

# SQLite Misc

## system tables

* sqlite_master
* sqlite_sequence
* sqlite_stat1

### sqlite_master
Master listing of all database objects in the database and the SQL used to create each object.

|Column|Description|
|----|----|
|type|type of object: table, index, trigger, view|
|name|name of object|
|tbl_name|table name associated with|
|rootpage|Root page|
|sql|DDL|

### sqlite_sequence
Lists the last sequence number used for the AUTOINCREMENT column in a table.

|Column|Description|
|----|----|
|name|table name associated with the AUTOINCREMENT column|
|seq|the last sequence number used|

### sqlite_state1
This table is created by the ANALYZE command to store statistical information about the tables and indexes analyzed. This information will be later used by the query optimizer.

|Column|Description|
|----|----|
|tbl|The table name that was analyzed|
|idx|The name of the index that was analyzed|
|stat|Information about the table and indexes analyzed that will be later used by the query optimizer|


## pragma

## sqlite3 commands
