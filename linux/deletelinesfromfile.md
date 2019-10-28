---
title: Delete lines from file
description: 
published: true
date: 2019-10-28T00:41:01.467Z
tags: 
---

# With sed

To delete lines 2, 12-17 and line 57 from file data.txt using sed you could do something like this:


```sh
sed -e '2d;12,17d;57d' data.txt > newfile.txt
```

To create a backup of the original file (with a .bak extension) use -i.bak with the command.

```sh
sed -i.bak -e '2d;12,17d;57d' data.txt
```
