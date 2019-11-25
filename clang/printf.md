---
title: printf, snprintf and other print functions in C
description: printf
published: true
date: 2019-11-25T03:11:51.145Z
tags: 
---

# printf
## printf in hex

```c

#include <stdio.h>

int main(){
    
    long val = 4478;

    printf("%lx\n", val);   // gives 117e
    printf("%x\n", 4479);   // gives 117f
    printf("%04x\n", 4779); // gives 12ab
    printf("%04X\n", 4779); // gives 12AB

    return 0;
}
```