---
title: Strace
description: 
published: true
date: 2019-10-28T00:42:13.648Z
tags: 
---

# By Pid

-p = pid
-s = show strings with until 9024 chars


```text
sudo strace -p 1234 -s9024
```


# Java application

```text
sudo strace -F -p 1234
```

# To trace child process that's fork()ed.
```text
strace -f 
```
