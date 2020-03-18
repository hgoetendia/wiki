---
title: Netcat
description: 
published: true
date: 2020-03-18T03:28:58.038Z
tags: 
---

# Netcat TCP server (forever listen) without -k option

```sh
#!/bin/bash

port=6700

while true;
do
    nc -l -p $port
    # WITH RESPONSE
    # echo -e "HELLO WORLD" | nc -l -p $port
done
exit 0

```
