---
title: String to long in C strtol
description: strtol
published: true
date: 2019-11-25T02:54:17.281Z
tags: 
---

# Example
```c
/**
 * C program to convert string to long using strtol() library function.
 */

#include <stdio.h>
#include <stdlib.h>     // Used for strtol()


int main()
{
    char number[30];
    char* end_ptr;

    long big_number;
    int base;


    /* Input string representation of number from user. */
    printf("Enter any number: ");
    fgets(number, 30, stdin);

    /* Input base */
    printf("Enter base: ");
    scanf("%d", &base);


    /* Convert string representation of number to long */
    big_number = strtol(number, &end_ptr, base);

    /* endPtr points to NULL for failed conversions */
    if(*end_ptr)
        printf("Unable to convert '%s' to base %d.", number, base);
    else
        printf("Converted long = %ld\n", big_number);


    return 0;
}```