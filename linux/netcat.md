---
title: Netcat
description: 
published: true
date: 2019-10-28T00:41:30.760Z
tags: 
---

# Netcat TCP server (forever listen) without -k option

```sh
#!/bin/bash

port=6700

while true;
do
    nc -l -p $port
done
exit 0

```
