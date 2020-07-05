---
title: Replication / Dump and restore
description: 
published: true
date: 2020-07-05T20:29:42.309Z
tags: mysqldump, replication, master, slave
---

# take snapshot for slave (all databases).
```bash
mysqldump -umyuser -pmypassword --all-databases --flush-logs --master-data=1 | gzip > all.masterNode_20190212.dmp.gz
```


# take snapshot for slave (some databases).

```bash
mysqldump -umyuser -pmypassword --databases myDB1 myDB2 --flush-logs --master-data=1 | gzip > all.masterNode_20190212.dmp.gz
```


hint:
```bash
zcat all.masterNode_20200705.dmp.gz|grep MASTER_LOG_FILE 
CHANGE MASTER TO MASTER_LOG_FILE='unfile-binlog.954868', MASTER_LOG_POS=106;
```
