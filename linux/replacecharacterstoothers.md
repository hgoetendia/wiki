---
title: Replace characters to others
description: 
published: true
date: 2019-10-28T00:41:48.963Z
tags: 
---

# Replace pipe to coma ( | to , )


```sh
sed 's/|/,/g' filewithpipes.txt  > filewithcomas.csv
```

# Replace tab with coma ( TAB to CSV )
```sh
$ cat data.tsv | tr "\\t" "," > data.csv
```