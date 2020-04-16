---
title: AWK
description: AWK hacks
published: true
date: 2020-04-16T18:52:12.802Z
tags: 
---

# AWK


## Field separator 

```
awk -F "," '{print $1}' filename
awk -F ":" '{print $4 "|" $6 "|" $7 "|" $5}'
```
