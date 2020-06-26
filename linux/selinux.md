---
title: SELinux
description: 
published: true
date: 2020-06-26T18:18:46.577Z
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
