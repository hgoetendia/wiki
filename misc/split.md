---
title: Split
description: A quick summary of Split
published: true
date: 2019-10-28T00:43:16.409Z
tags: 
---

# Split a file into equal parts, without breaking individual lines

l = Leter L

```sh
split -n l/5 your_file.txt

```

no need for scripting here.

From the man file, CHUNKS  may  be:

l/N     split into N files without splitting lines

Or use (split every 75 lines)

```sh
split --lines=75 your_file.txt
```
