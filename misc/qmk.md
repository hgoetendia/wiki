---
title: QMK Massdrop DROP CTRL configuration
description: Customize Massdrop DROP CTRL Mechanic Keyboard 
published: true
date: 2020-11-20T23:54:49.778Z
tags: qmk, keyboard, mechanic, drop, ctrl, drop ctrl
---

# Setup QMK

```bash
$ python3.8 -m pip install --user qmk
$ qmk setup
$ qmk compile -kb massdrop/ctrl -km default
$ ls -lah qmk_firmware/massdrop_ctrl_default.bin
```