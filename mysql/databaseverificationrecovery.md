---
title: Database verification recovery
description: A quick summary of Databaseverificationrecovery
published: true
date: 2019-10-28T00:43:46.200Z
tags: 
---

# Avoid database verification recovery

* Start database withouth innoDB verification/recovery
Add in `/etc/my.cnf.d/server.cnf` the line

```text
innodb_force_recovery = 1
```
