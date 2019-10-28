---
title: Remove lines included in one file from another file
description: 
published: true
date: 2019-10-28T00:41:42.445Z
tags: 
---

```sh
grep -Fvx -f partial.list complete.list >remaining.list
```
