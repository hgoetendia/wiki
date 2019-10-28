---
title: Fork
description: A quick summary of Fork
published: true
date: 2019-10-28T00:46:48.738Z
tags: 
---

# Fork

```python
import os

newpid = os.fork()

if newpid == 0:
   #Child
   pass 
else:
   #Father
   pids = (os.getpid(), newpid)
   print("parent: %d, child: %d\n" % pids)
```

   