---
title: Misco
description: 
published: true
date: 2020-12-17T20:49:44.151Z
tags: postgresql, select tables , query, querys
---

# Get tables by name

``` sql
SELECT 
    table_schema,
    table_name
FROM 
    information_schema.tables
WHERE 
    table_name like '%sometable%' AND
    table_schema not in ('information_schema', 'pg_catalog') AND
    table_type = 'BASE TABLE'
ORDER BY
    table_name,
    table_schema;
```

# Select yesterday

``` sql
SELECT DATE( NOW() - INTERVAL '1 day');
```

# Query show/hide table headers

Use the flag `-t`

```sql
$ psql -t myDatabase

myDatabase=# SELECT DATE( NOW() - INTERVAL '1 day');
 2020-12-16

myDatabase=#

$ psql myDatabase
myDatabase=# SELECT DATE( NOW() - INTERVAL '1 day');
    date
------------
 2020-12-16
(1 row)
myDatabase=#
```