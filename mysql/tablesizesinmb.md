---
title: Table sizes in MB
description: 
published: true
date: 2019-10-28T00:44:44.691Z
tags: 
---

```sql
SELECT 
     table_schema as `Database`, 
     table_name AS `Table`, 
     round(((data_length + index_length) / 1024 / 1024), 2) `Size in MB` 
FROM information_schema.TABLES 
ORDER BY (data_length + index_length) DESC;
```
