---
title: Index
description: 
published: true
date: 2019-10-28T00:46:13.555Z
tags: 
---

# Show table index 


```pgsql
postgres=> SELECT * FROM pg_indexes WHERE tablename = 'mytable';

 schemaname | tablename |       indexname        | tablespace |                                  indexdef                                  
------------+-----------+------------------------+------------+----------------------------------------------------------------------------
 public     | mytable   | myoriginalindex        |            | CREATE UNIQUE INDEX myoriginalindex ON scoring USING btree (myTableId)

```

# Alter index
## Rename

```pgsql
postgres=> ALTER index myoriginalindex rename to newindex;
```
