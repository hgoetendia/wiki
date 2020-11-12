---
title: Postgres Extensions
description: 
published: true
date: 2020-11-12T23:26:45.219Z
tags: extensions, postgres, uuid
---

# UUID


```sh
$ psql
Type "help" for help.
postgres=# \c mydatabase
You are now connected to database "mydatabase" as user "postgres".
mydatabase=# CREATE EXTENSION "uuid-ossp";
CREATE EXTENSION
hermes=# SELECT uuid_generate_v1();
           uuid_generate_v1
--------------------------------------
 a3a92048-253d-11eb-b9ec-7f15ea97cce5
(1 row)

mydatabase=#
```