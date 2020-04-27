---
title: Packages
description: Linux packages 
published: true
date: 2020-04-27T16:25:34.541Z
tags: deb, dpkg, apt, yum, rpm
---

# Debian

## List installed packages

```
sudo apt list --installed
```
```
dpkg --get-selections | grep -v deinstall
```
```
sudo dpkg-query -l
```