---
title: Redis
description: REDIS
published: true
date: 2020-07-23T00:02:38.501Z
tags: redis, nosql
---

# Redis
Your content here


# Duplicate service in Debian

```
cp /etc/redis/redis.conf /etc/redis/redis_second.conf
chown redis.redis /etc/redis/redis_second.conf
```

```
root@portalgaming-machine-1:/etc/redis# diff redis.conf redis_second.conf
84c84
< port 6379
---
> port 6380
150c150
< pidfile /var/run/redis/redis-server.pid
---
> pidfile /var/run/redis/redis-server_second.pid
163c163
< logfile /var/log/redis/redis-server.log
---
> logfile /var/log/redis/redis-server_second.log
247c247
< dir /var/lib/redis
---
> dir /var/lib/redis_second

```
```
cp /lib/systemd/system/redis-server.service /lib/systemd/system/redis-server_second.service

root@portalgaming-machine-1:/etc/redis# diff /lib/systemd/system/redis-server.service  /lib/systemd/system/redis-server_second.service
8,9c8,9
< ExecStart=/usr/bin/redis-server /etc/redis/redis.conf
< PIDFile=/var/run/redis/redis-server.pid
---
> ExecStart=/usr/bin/redis-server /etc/redis/redis_second.conf
> PIDFile=/var/run/redis/redis-server_second.pid
28c28
< ReadWriteDirectories=-/var/lib/redis
---
> ReadWriteDirectories=-/var/lib/redis_second
40c40
< Alias=redis.service
---
> Alias=redis_second.service

```
```
mkdir /var/lib/redis_second
chown  redis.redis /var/lib/redis_second
```
```
systemctl enable redis-server_second.service
systemctl start redis-server_second.service
```

# Log In
```
$ redis-cli
```

# Show keys
```
127.0.0.1:6379[1]> keys *
```

# Delete/Drop all keys
```
127.0.0.1:6379[1]> flushdb
```
