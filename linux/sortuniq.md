---
title: Sort uniq
description: A quick summary of Sortuniq
published: true
date: 2020-07-22T18:06:51.508Z
tags: sort, uniq, duplicados, duplicates
---

# Unique lines


```sh
$ uniq -u < file
```


# Couting unique lines


```sh
unixite@sandbox:~$ cat test.txt
one
one
one
two
two
one
five
one
one
two
five
two
one
one
one
two
two
one
five
one
one
two
three
four
two
five
unixite@sandbox:~$ sort test.txt  | uniq -c
      4 five
      1 four
     12 one
      1 three
      8 two
unixite@sandbox:~$ sort test.txt  | sort -n -r | uniq -c 
     12 one
      8 two
      4 five
      1 three
      1 four
unixite@sandbox:~$
```
