---
title: Mysql delete 
description: 
published: true
date: 2019-11-19T21:46:59.171Z
tags: 
---

# Delete rows based on another table

```sql
delete t from table_tmp t, borra b where t.id=b.smpp_message_id;
```