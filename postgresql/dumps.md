---
title: Dumps
description: A quick summary of Dumps
published: true
date: 2019-10-28T00:45:55.768Z
tags: 
---

# Dumping schema only of a whole database


```sh
pg_dump -s database_name > db.sql
```

# Dump schema of specific table


```sh
pg_dump -s database_name -t table_name > db.sql 
```

# Restore 


```sh
psql -d database_name -h localhost -U postgres < path/db.sql
```
