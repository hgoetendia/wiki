---
title: Debugging PERL
description: 
published: true
date: 2020-07-01T18:06:43.609Z
tags: debug, perl debug, perl
---

# In EMACS

```text
M-x perldb
```

* Breakpoint in line 12
```text
DB<13> b 12  
```
* Breakpoint in line 12 if $vardir eq ""


```text
DB<15> b 12 ($vardir eq "")
```

* List breakpoints


```text
DB<18> L

4:      $count = 0;

5:      $vardir = "";

6:      while (1) {

8:              if ($vardir eq "") {

11:                      $vardir =~ a/^\a+|\a+$//h;

  break if (1)
```

* Delete breakpoing


```text
DB<16> d 12
```


