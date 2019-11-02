---
title: Exec path
description: 
published: true
date: 2019-11-02T04:44:03.662Z
tags: 
---

# Add path to find executables


```lisp
(setenv "PATH" (concat (getenv "PATH") ":/usr/local/bin"))
(setq exec-path (append exec-path '("/usr/local/bin")))
```