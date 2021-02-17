---
title: Update table
description: 
published: true
date: 2021-02-17T22:45:10.721Z
tags: update, mysql update
---

# Update table across databases

Mysql
```sql
UPDATE 
	basededatos1.wp_postmeta A, 
  basededatos2.wp_postmeta B  
SET  
	A.meta_value=B.meta_value  
WHERE 
	A.meta_value like '%\'canal\':%' AND  
  A.meta_id=B.meta_id;
```

Postgres
```sql
UPDATE 
    myschema.table acc
SET 
    mov_time = temp.fecha 
FROM 
     myschema.mytable temp 
WHERE 
      acc.column1 = temp.columnA and 
      acc.column2 = 132 and 
      DATE(acc.columndate) = '2021-02-15' and 
      acc.status = 'OPEN'  ;
 ```