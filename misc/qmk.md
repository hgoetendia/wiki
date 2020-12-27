---
title: QMK Massdrop DROP CTRL configuration
description: Customize Massdrop DROP CTRL Mechanic Keyboard 
published: true
date: 2020-12-27T01:18:24.486Z
tags: qmk, keyboard, mechanic, drop, ctrl, drop ctrl
---

# Setup QMK

```bash
$ python3.8 -m pip install --user qmk
$ qmk setup
$ qmk compile -kb massdrop/ctrl -km default
$ ls -lah qmk_firmware/massdrop_ctrl_default.bin
```

# Install 
Download mdloader_linux from https://github.com/Massdrop/mdloader/releases for my case mdloader_linux

```bash
$ ls -lah qmk_firmware/massdrop_ctrl_default.bin
./mdloader_linux --first --download qmk_firmware/massdrop_ctrl_default.bin --restart
```