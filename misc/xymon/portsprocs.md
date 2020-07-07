---
title: Xymon Ports, Procs alarm
description: 
published: true
date: 2020-07-07T03:12:12.292Z
tags: xymon proc, xymon port
---

# In xymon server 


`File: analysis.cfg`

```bash
HOST=playserver
        PROC %mysqld
        PROC %smppserver*
        PROC %smppclient*
        PROC %controlhub*
        PROC %ws_aladin* min=3
        PROC %aladinevnot*
        PROC %modem_event_listener*
        PROC %mywebservice_9912*
        PROC %mywebservice* min=2
        PORT LOCAL=%[\.:](80) STATE=LISTEN min=1 TEXT=http
        #PORT LOCAL=%[\.:]80 STATE=ESTABLISHED min=0 TRACK=http TEXT=web
        PORT LOCAL=%[\.:]8080 STATE=LISTEN TEXT=tomcat
        PORT LOCAL=%[\.:]9911 STATE=LISTEN TEXT=wshttps
        PORT LOCAL=%[\.:]3306 STATE=LISTEN TEXT=mysql
        PORT LOCAL=%[\.:]9898 STATE=LISTEN TEXT=controlhub
HOST=gateway-server-gestion
        PROC %mysqld
        PORT LOCAL=%[\.:](80) STATE=LISTEN min=1 TEXT=http
        #PORT LOCAL=%[\.:]80 STATE=ESTABLISHED min=0 TRACK=http TEXT=web
        PORT LOCAL=%[\.:]3306 STATE=LISTEN TEXT=mysql
```