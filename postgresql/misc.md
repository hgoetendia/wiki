---
title: Misco
description: 
published: true
date: 2020-06-12T00:39:26.242Z
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