---
title: Replication
description: A quick summary of Replication
published: true
date: 2019-10-28T00:44:40.033Z
tags: 
---

# take snapshot for slave.
mysqldump -umyuser -pmypassword --all-databases --flush-logs --master-data=1 | gzip > all.masterNode_20190212.dmp.gz

Commando