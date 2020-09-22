---
title: Update table
description: 
published: true
date: 2020-09-22T23:53:24.485Z
tags: update, mysql update
---

# Update table across databases


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