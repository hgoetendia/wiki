---
title: Tmux
description: A quick summary of Tmux
published: true
date: 2020-07-04T22:50:08.346Z
tags: 
---

# Config file .tmux.conf


```bash
# Toggle mouse on
bind-key M \
  set-option -g mouse on \;\
  display-message 'Mouse: ON'

# Toggle mouse off
bind-key m \
  set-option -g mouse off \;\
  display-message 'Mouse: OFF'

# Sane scrolling
set -g terminal-overrides 'xterm*:smcup@:rmcup@'
set-option -g mouse on


set -g default-terminal "xterm-256color"

# Paste con clipboard
bind-key -n C-y \
  run "tmux set-buffer \"$(xclip -o -sel clipboard)\"; tmux paste-buffer" \;\
  display-message 'Pegando..'

# Copy con clipboard
bind-key -n  -T copy-mode M-w  \
  send-keys -X copy-pipe-and-cancel  "tmux save-buffer - | xclip -i -selection clipboard > /dev/null 2>&1" \;\
  display-message 'Copiando..'
#set -g set-clipboard on

# History
set-option -g history-limit 100000


######################
### DESIGN CHANGES ###
######################

# loud or quiet?
#set -g visual-activity off
#set -g visual-bell off
#set -g visual-silence off
#setw -g monitor-activity off
#set -g bell-action none

#  modes
setw -g clock-mode-colour colour5
setw -g mode-style 'fg=colour1 bg=colour18 bold'

# panes
set -g pane-border-style 'fg=colour19 bg=colour0'
set -g pane-active-border-style 'bg=colour0 fg=colour9'

# statusbar
set -g status-position bottom
set -g status-justify left
set -g status-style 'bg=colour18 fg=colour255 dim'
set -g status-left ''
set -g status-right '#[fg=colour255,bg=colour19] %d/%m #[fg=colour255,bg=colour19] %H:%M:%S '
set -g status-right-length 50
set -g status-left-length 20

#setw -g window-status-current-style 'fg=colour1 bg=colour23 bold'
setw -g window-status-current-style 'fg=colour1 bg=colour23'

setw -g window-status-current-format ' #I#[fg=colour249]:#[fg=colour255]#W#[fg=colour249]#F '

setw -g window-status-style 'fg=colour9 bg=colour18'
setw -g window-status-format ' #I#[fg=colour237]:#[fg=colour250]#W#[fg=colour244]#F '

setw -g window-status-bell-style 'fg=colour255 bg=colour1 bold'

# messages
set -g message-style 'fg=colour255 bg=colour16 bold'

```


Personal conf:

```bash
############################
###  TMUX PERSONAL CONF  ###
###        BY HGB        ###
############################

# Toggle mouse on
bind-key M \
  set-option -g mouse on \;\
  display-message 'Mouse: ON'

# Toggle mouse off
bind-key m \
  set-option -g mouse off \;\
  display-message 'Mouse: OFF'

# Sane scrolling
set -g terminal-overrides 'xterm*:smcup@:rmcup@'
set-option -g mouse on


set -g default-terminal "xterm-256color"

#Ambas necesitan tener el xclip instalado en el SO
# Paste con clipboard
bind-key -n C-y \
  run "tmux set-buffer \"$(xclip -o -sel clipboard)\"; tmux paste-buffer" \;\
  #display-message 'Pegando..'

# Copy con clipboard
bind-key -n  -T copy-mode M-w  \
  send-keys -X copy-pipe-and-cancel  "tmux save-buffer - | xclip -i -selection clipboard > /dev/null 2>&1" \;\
  #display-message 'Copiando..'
set -g set-clipboard on

# History
set-option -g history-limit 100000


######################
### DESIGN CHANGES ###
######################


#set -g @online_icon "ok"
#set -g @offline_icon "offline!"
set -g status-interval 5


# loud or quiet?
#set -g visual-activity off
#set -g visual-bell off
#set -g visual-silence off
#setw -g monitor-activity off
#set -g bell-action none

#  modes
setw -g clock-mode-colour colour5
setw -g mode-style 'fg=colour1 bg=colour18 bold'

# panes
set -g pane-border-style 'fg=colour19 bg=colour0'
set -g pane-active-border-style 'bg=colour0 fg=colour9'

# statusbar
set -g status-position bottom
set -g status-justify left
set -g status-style 'bg=colour19 fg=colour255 dim'
set -g status-left ''
set -g status-right '#[fg=colour255,bg=colour20] TiaxaVPN:#{tiaxavpn_status} Internet:#{online_status}  %d/%m #[fg=colour255,bg=colour20] %H:%M:%S '
set -g status-right-length 50
set -g status-left-length 20

#setw -g window-status-current-style 'fg=colour1 bg=colour23 bold'
setw -g window-status-current-style 'fg=colour46 bg=colour23'

setw -g window-status-current-format ' #I#[fg=colour249]:#[fg=colour255]#W#[fg=colour249]#F '

setw -g window-status-style 'fg=colour10 bg=colour18'
setw -g window-status-format ' #I#[fg=colour237]:#[fg=colour250]#W#[fg=colour249]#F '

setw -g window-status-bell-style 'fg=colour255 bg=colour1 bold'

# messages
set -g message-style 'fg=colour255 bg=colour16 bold'

# Personal scripts launch
#run-shell /home/horacio/tmuxplugins/tmuxonline/online_status.tmux
#run-shell /home/horacio/tmuxplugins/tmuxtiaxavpn/online_status.tmux
```