---
title: Errno
description: A quick summary of Errno
published: true
date: 2019-10-28T00:38:49.627Z
tags: 
---

```c_cpp

#include <stdio.h>
#include <string.h>
#include <errno.h>

int main ()
{
    FILE * pFile;
    pFile = fopen ("foounexist.file","r");
    if (pFile == NULL)
        printf ("Error opening file: %s\n",strerror(errno));
    return 0;
}
```
