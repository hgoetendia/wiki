---
title: Valgrind
description: A quick summary of Valgrind
published: true
date: 2019-10-28T00:43:30.823Z
tags: 
---

# Check memory leakings

```sh
$ valgrind --leak-check=full --show-leak-kinds=all --track-origins=yes --verbose --log-file=valgrind-out.txt ./executable exampleParam1
```
