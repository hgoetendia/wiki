---
title: Postgresql Activity
description: 
published: true
date: 2020-07-22T18:22:36.338Z
tags: activity, show process, show processlist, pg_activity
---


# PostgreSQL activity

MySQL has a very powerfull command through “show full processlist;", to see a list of currently running queries: `show full processlist;`

PostgreSQL has a similar shell to MySQL, named psql. Here’s how it works. First, change to the postgres user.
```
# su postgres
# [postgres@srv]$ psql
postgres=# select * from pg_stat_activity;
```




This requires you have PostgreSQL configured to enable logging.  Edit your PostgreSQL config file (usually at /usr/local/pgsql/data/postgresql.conf), and add the following line.

```
stats_command_string = true
```
And reload your PostgreSQL.
```
pg_ctl reload
```