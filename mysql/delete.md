---
title: Mysql delete 
description: 
published: true
date: 2020-12-23T21:15:37.027Z
tags: 
---

# Delete rows based on another table

```sql
DELETE 
	t 
FROM 
	table_tmp t, 
  borra b 
WHERE 
	t.id=b.smpp_message_id;
```