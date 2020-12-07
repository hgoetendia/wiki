---
title: Schemas
description: 
published: true
date: 2020-12-07T22:55:52.505Z
tags: 
---

# Create schema

```pgsql
[local]postgres@postgres=# CREATE SCHEMA myschema;
```


# Add schema to search path


```bash
mydatabase=> SHOW search_path;
   search_path
-----------------
 "$user", public
(1 row)
mydatabase=> SET search_path TO "$user", public, config;
SET
mydatabase=> SHOW search_path;
       search_path
-------------------------
 "$user", public, config
(1 row)

mydatabase=>
```

Another example:

```
myDatabase=> ALTER DATABASE myDatabase SET search_path =  "$user",  work, config, public;
```