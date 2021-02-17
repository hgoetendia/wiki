---
title: AWK
description: AWK hacks
published: true
date: 2021-02-17T21:41:46.488Z
tags: awk
---

# AWK


## Field separator 

```
awk -F "," '{print $1}' filename
awk -F ":" '{print $4 "|" $6 "|" $7 "|" $5}'
head  myfile.ssv|awk -F ";" '{print $1 "|" $2 "|" $3 "|" substr($4,1,4) "-" substr($4,5,2) "-" substr($4,7,2) " " substr($4,9,2) ":"  substr($4,11,2) ":" substr($4,13,2)}'
```
