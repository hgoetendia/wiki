---
title: Netcat
description: 
published: true
date: 2021-07-20T21:10:59.756Z
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
Echo server

```sh
#!/bin/bash

port=3010

while true;
do
    echo "hola mundo"
    nc -l -p $port -c 'read i && echo $i;'

done
exit 0
```