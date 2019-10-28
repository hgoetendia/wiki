---
title: Tablespace
description: 
published: true
date: 2019-10-28T00:46:33.234Z
tags: 
---

# Create tablespace
`/path/to/example/directory'` must have postgres user perms

```pgsql
[local]postgres@postgres=# CREATE TABLESPACE mitablespace LOCATION '/path/to/example/directory';

```

# Show tablespaces


```pgsql
[local]postgres@postgres=#\db
                Listado de tablespaces
    Nombre    |  Dueño   |         Ubicación          
--------------+----------+----------------------------
 pg_default   | postgres | 
 pg_global    | postgres | 
 mitablespace | postgres | /path/to/example/directory
(3 filas)

```
