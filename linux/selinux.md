---
title: SELinux
description: 
published: true
date: 2020-07-04T00:47:02.967Z
tags: selinux
---

# Check the SELinux status

```
sudo getenforce
```

More verbose

```
sudo sestatus
```

Suitable for programming:

```
sudo selinuxenabled
if [ $? -ne 0 ]
then 
    echo "DISABLED"
else
    echo "ENABLED"
fi
```



#  Help
```
setenforce 
usage:  setenforce [ Enforcing | Permissive | 1 | 0 ]
```

# Disable SELinux
```
sudo setenforce 0
```
or
```
sudo setenforce Permissive
```

# Enable SELinux

```
sudo setenforce 1
```

```
sudo setenforce Enforcing
```
