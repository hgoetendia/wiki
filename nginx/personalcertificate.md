---
title: Create self signed certificate
description: 
published: true
date: 2020-12-22T00:27:21.755Z
tags: certificate, personal certificate
---

# Header
Your content here


```sh
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.cer
```