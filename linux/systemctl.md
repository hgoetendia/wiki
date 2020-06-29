---
title: Services using systemctl
description: 
published: true
date: 2020-06-29T14:51:14.035Z
tags: sytemctl, service, services
---

# Systemctl

## List
```
sudo systemctl list-units --type=service
```
Or
```
sudo systemctl --type=service
```

## Stop
```
sudo systemctl stop mysql
```
## Start
```
sudo systemctl start mysql
```
## Disable to prevent automatic start on boot.
```
sudo systemctl disable mysql
```
