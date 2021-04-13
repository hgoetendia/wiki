---
title: lsof
description: 
published: true
date: 2021-04-13T22:58:15.634Z
tags: lsof
---

# LSOF

## Print all related a PID

-P : To print numeric ports.
-p : Process PID

```bash
lsof  -P  -p 16517
```

## Find and remove large files that are open but have been deleted


```bash
lsof -a +L1 /tmp
lsof -a +L1
```


### To save it:

This awesomeness was introduced to ln in v8.0 (GNU/coreutils) with the -L|--logical option which causes ln to dereference a /proc/<pid>/fd/<handle> first. So a simple
  
```bash
ln -L /proc/<pid>/fd/<handle> /path/to/deleted/file
  ```
  
You can use debugfs. Run this command within:

```bash
ln <$INODE> FILENAME
```
  
### To truncate it:

```bash
: > /path/to/the/file.log
```

If it was already deleted, on Linux, you can still truncate it by doing:

```bash
: > "/proc/$pid/fd/$fd"
```
