---
title: Users
description: 
published: true
date: 2020-07-03T16:55:43.762Z
tags: create user, adduser, user
---

# Create a user.

```sh
sudo adduser juan
sudo passwd juan
```

# Add the user to group.
In this case we will user the `wheel` group:


```sh
sudo usermod -aG wheel juan
```

For interact with serial devices ( dialout ) group
```sh
sudo usermod -aG dialout juan
```

In UBUNTU


```sh
sudo gpasswd -a tiaxa dialout
```


All commands were tested in Centos.

# Show user groups belongs to


```sh
$ groups
```

