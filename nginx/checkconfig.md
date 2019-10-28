---
title: Nginx Basic commands
description: 
published: true
date: 2019-10-28T00:44:59.344Z
tags: 
---

# Install Nginx 

Centos/RedHat
```sh
sudo yum install -y nginx
```

# Enable and start Nginx. 

Centos/RedHat

```sh
sudo systemctl enable nginx.service
sudo systemctl start nginx.service
```

# Check the configuration.

```sh
sudo nginx -t
```

# Reload Nginx.
Centos/RedHat

```sh
sudo systemctl reload nginx.service
```

