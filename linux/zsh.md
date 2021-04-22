---
title: ZSH
description: 
published: true
date: 2021-04-22T18:07:08.477Z
tags: zsh, prezto
---

# zsh

```sh
sudo apt-get install zsh
```

## Prezto

Launch `zsh`

```sh
git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"
```

Execute this:

```sh
setopt EXTENDED_GLOB
for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
  ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
done
```

Change default shell

```sh
chsh -s /bin/zsh
```