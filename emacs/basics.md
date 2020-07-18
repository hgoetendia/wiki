---
title: Emacs/Basics
description: 
published: true
date: 2020-07-18T22:48:26.531Z
tags: 
---

# Install
Default emacs package in Centos 7.5 is Emacs 24.3.1

```sh
sudo yum install -y emacs
```

If you prefer other versions you can install it from sources:

Example: Emacs 26.1

```sh
sudo yum -y install libXpm-devel libjpeg-turbo-devel openjpeg-devel openjpeg2-devel turbojpeg-devel giflib-devel libtiff-devel gnutls-devel libxml2-devel GConf2-devel dbus-devel wxGTK-devel gtk3-devel wget gcc ncurses-devel.x86_64
wget http://git.savannah.gnu.org/cgit/emacs.git/snapshot/emacs-26.1.tar.gz
tar zxvf emacs-26.1.tar.gz
cd emacs-26.1
./autogen.sh
./configure --without-makeinfo # incase makeinfo is not available on your system: Example Centos 7 else `./configure` would do
sudo make install
```

Check version


```sh
emacs --version
GNU Emacs 26.1
```




To start emacs
```sh
emacs
```

# .emacs file

Create startup configuration file `.emacs`


```lisp
emacs .emacs
```



![Filedotemacs](/uploads/emacs/filedotemacs.png "Filedotemacs")

# Inhibit initial splash screen


```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;Inhibir splash screen;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq inhibit-splash-screen t)
```


# Repos

 Repo `gnu` and `melpa` to install emacs addons.
 

```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;Paquetes para instalar;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(package-initialize)
(setq package-archives '(("gnu" . "https://elpa.gnu.org/packages/")
                         ("melpa" . "https://melpa.org/packages/")))

```

To show package list: `M-x package-list-packages`

![Packages](/uploads/emacs/packages.png "Packages")

## Install package

Example:

`M-x package-install`

`Install package: yasnippet`


# Backup folder
Set the backup folder to avoid them.


```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;Para que todos los archivos backup residan en un solo sitio;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq backup-directory-alist `(("." . "~/")))

```

# Default directory

```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;Directorio por defecto;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq default-directory "~/")

```

# Resize windows

With keys:

* F7 Enlarge window horizontally
* F8 Shrink window horizontally
* F9 Enlarge window vertically
* F10 Shrink window vertically

```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;Resize de ventanas con las teclas F;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;; Use control-arrow keys for window resizing
(global-set-key [f7] 'enlarge-window-horizontally)
(global-set-key [f8] 'shrink-window-horizontally)
(global-set-key [f9] 'enlarge-window)
(global-set-key [f10] 'shrink-window)

```


# Switching between windows

Custom switching using:

* ESC left arrow
* ESC right arrow
* ESC up arrow
* ESC down arrow


```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;Navegacion por ventanas con el cursor y escape;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(global-set-key (kbd "ESC <left>") 'windmove-left)          ; move to left window
(global-set-key (kbd "ESC <right>") 'windmove-right)        ; move to right window
(global-set-key (kbd "ESC <up>") 'windmove-up)              ; move to upper window
(global-set-key (kbd "ESC <down>") 'windmove-down)          ; move to lower window
```

# Match parentesis


```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;Para ver los parentesis que corresponden usando % sobre el simbolo;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(show-paren-mode t)

(global-set-key "%" 'match-paren)
          
          (defun match-paren (arg)
            "Go to the matching paren if on a paren; otherwise insert %."
            (interactive "p")
            (cond ((looking-at "\\s(") (forward-list 1) (backward-char 1))
                  ((looking-at "\\s)") (forward-char 1) (backward-list 1))
                  (t (self-insert-command (or arg 1)))))

```

# Return to the previously edit position
When you visit a file, point goes to the last place where it was when you previously visited the same file.

For GNU Emacs 24.5 and older versions

```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;; A la hora de cargar te devuelva a la misma posicion donde estabas;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(require 'saveplace)
(setq-default save-place t)
```

For GNU Emacs 25.1 and newer versions
```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;; A la hora de cargar te devuelva a la misma posicion donde estabas;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(save-place-mode 1) 
```


# Show column number

```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;Para ver en que columna estas;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq column-number-mode t)
```


# Neotree (file manager)
F12 to toggle neotree window

![Installneotree](/uploads/emacs/installneotree.png "Installneotree")

```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;NEOTREE directorios a la izquierda;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(require 'neotree)
  (global-set-key [f12] 'neotree-toggle)

```


![Neotree 2](/uploads/emacs/neotree-2.png "Neotree 2")


# Fix MacOSX meta key issue


```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;Cambiamos la tecla meta alt a q no tenga funcion esto para MACOS;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq mac-option-modifier nil)

```

# Look and feel

```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;Look And Feel ( Coloreado );;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(default ((t (:inherit nil :stipple nil :background "gray0" :foreground "green"
			 :inverse-video nil :box nil :strike-through nil
			 :overline nil :underline nil :slant normal
			 weight normal :width normal :family "monospace"))))
 '(background "black")
 '(font-lock-builtin-face ((((class color) (background dark))
			    (:foreground "Turquoise"))))
 '(font-lock-comment-face ((t (:foreground "red"))))
 '(font-lock-constant-face ((((class color) (background dark))
			     (:bold t :foreground "DarkOrchid"))))
 '(font-lock-doc-string-face ((t (:foreground "yellow"))))
 '(font-lock-function-name-face ((t (:foreground "green1"))))
 '(font-lock-keyword-face ((t (:foreground "DeepSkyBlue"))))
 '(font-lock-preprocessor-face ((t (:italic nil :foreground "CornFlowerBlue"))))
 '(font-lock-reference-face ((t (:foreground "DodgerBlue"))))
 '(font-lock-string-face ((t (:foreground "gold2")))))
```

## Mark selected text


```lisp
;;;;;;;;Para que aparezca coloreado cuando seleccionas un texto
(transient-mark-mode t)

```

## Comments in blue

```lisp
;;;;;;;;;;;;;;;;;;;;;;;;Comentario en azul;
(set-face-foreground 'font-lock-comment-face "Red" )
(set-variable font-lock-comment-face 'font-lock-comment-face)
```


## Window margin
```lisp
;;;;;;;;;;;;;;;;;;;;;;;;Left/Right window margin;;;;;;;;;;;
 (setq-default left-margin-width 1 right-margin-width 1) ; Define new widths.
 (set-window-buffer nil (current-buffer)) ;; Use them now.
```


## Line numbers 


```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;Line numbers in code        ;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;(global-linum-mode 1)
(add-hook 'prog-mode-hook 'linum-mode)
;(setq linum-format "%4d \u2502 ") ;With vertical bar
(setq linum-format "%d ")
```

## Winner Mode                                                                                                                                                                      

```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;; Winner mode : Undo window operations;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(winner-mode 1)
```



## Extras

When press key 'End' and shows get an error `<select> is undefined`


```lisp
;; PuTTY fix. Ugly. Bad. But it works. (Good)
;; Even when TERM=xterm-256color on bash and
;; ~/.tmux.conf says:
;;   set-window-option -g xterm-keys on
;;   set -g default-terminal "xterm-256color"
;; still, pressing < end > key results in error:
;;   < select > is undefined
;; This hack fixes the end key. Home key already
;; worked on Linux/tmux (don't know about putty)
;;
(define-key global-map "\M-[1~" 'beginning-of-line)
(define-key global-map [select] 'end-of-line)
```


# All together


```lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;Inhibir splash screen;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq inhibit-splash-screen t)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;Para que todos los archivos backup residan en un solo sitio;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq backup-directory-alist `(("." . "~/.emacs.d/backup")))

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;Paquetes para instalar;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(package-initialize)
(setq package-archives '(("gnu" . "https://elpa.gnu.org/packages/")
                         ("melpa" . "https://melpa.org/packages/")))


;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;Resize de ventanas con las teclas F;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;; Use control-arrow keys for window resizing
(global-set-key [f7] 'enlarge-window-horizontally)
(global-set-key [f8] 'shrink-window-horizontally)
(global-set-key [f9] 'enlarge-window)
(global-set-key [f10] 'shrink-window)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;Navegacion por ventanas con el cursor y escape;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(global-set-key (kbd "ESC <left>") 'windmove-left)        ; move to left window
(global-set-key (kbd "ESC <right>") 'windmove-right)      ; move to right window
(global-set-key (kbd "ESC <up>") 'windmove-up)            ; move to upper window
(global-set-key (kbd "ESC <down>") 'windmove-down)        ; move to lower window

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;; A la hora de cargar te devuelva a la misma posicion donde estabas;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(require 'saveplace)
(save-place-mode 1) 


;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;Para ver los parentesis que corresponden usando % sobre el simbolo;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(show-paren-mode t)

(global-set-key "%" 'match-paren)
          
          (defun match-paren (arg)
            "Go to the matching paren if on a paren; otherwise insert %."
            (interactive "p")
            (cond ((looking-at "\\s(") (forward-list 1) (backward-char 1))
                  ((looking-at "\\s)") (forward-char 1) (backward-list 1))
                  (t (self-insert-command (or arg 1)))))


;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;Para ver en que columna estas;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq column-number-mode t)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;NEOTREE F12 y directorios a la izquierda;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(require 'neotree)
  (global-set-key [f12] 'neotree-toggle)
	
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;Cambiamos la tecla meta alt a q no tenga funcion esto para MACOS;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq mac-option-modifier nil)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;Look And Feel ( Coloreado );;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(default ((t (:inherit nil :stipple nil :background "gray0" :foreground "green"
			 :inverse-video nil :box nil :strike-through nil
			 :overline nil :underline nil :slant normal
			 weight normal :width normal :family "monospace"))))
 '(background "black")
 '(font-lock-builtin-face ((((class color) (background dark))
			    (:foreground "Turquoise"))))
 '(font-lock-comment-face ((t (:foreground "red"))))
 '(font-lock-constant-face ((((class color) (background dark))
			     (:bold t :foreground "DarkOrchid"))))
 '(font-lock-doc-string-face ((t (:foreground "yellow"))))
 '(font-lock-function-name-face ((t (:foreground "green1"))))
 '(font-lock-keyword-face ((t (:foreground "DeepSkyBlue"))))
 '(font-lock-preprocessor-face ((t (:italic nil :foreground "CornFlowerBlue"))))
 '(font-lock-reference-face ((t (:foreground "DodgerBlue"))))
 '(font-lock-string-face ((t (:foreground "gold2")))))

;;;;;;;;Para que aparezca coloreado cuando seleccionas un texto
(transient-mark-mode t)
;;;;;;;;;;;;;;;;;;;;;;;;Comentario en azul;
(set-face-foreground 'font-lock-comment-face "Red" )
(set-variable font-lock-comment-face 'font-lock-comment-face)

;;;;;;;;;;;;;;;;;;;;;;;;Left/Right window margin;;;;;;;;;;;
 (setq-default left-margin-width 1 right-margin-width 1) ; Define new widths.
 (set-window-buffer nil (current-buffer)) ;; Use them now.

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;Line numbers in code        ;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;(global-linum-mode 1)
(add-hook 'prog-mode-hook 'linum-mode)
;(setq linum-format "%4d \u2502 ") ;With vertical bar
(setq linum-format "%d ")

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;; Winner mode : Undo window operations;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(winner-mode 1)


;; PuTTY fix. Ugly. Bad. But it works. (Good)
;; Even when TERM=xterm-256color on bash and
;; ~/.tmux.conf says:
;;   set-window-option -g xterm-keys on
;;   set -g default-terminal "xterm-256color"
;; still, pressing < end > key results in error:
;;   < select > is undefined
;; This hack fixes the end key. Home key already
;; worked on Linux/tmux (don't know about putty)
;;
(define-key global-map "\M-[1~" 'beginning-of-line)
(define-key global-map [select] 'end-of-line)

```




# Personal Setting
``` lisp
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;Inhibir splash screen;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq inhibit-splash-screen t)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;Para que todos los archivos backup residan en un solo sitio;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq backup-directory-alist `(("." . "~/.emacs.d/backup")))

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;Paquetes para instalar;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(package-initialize)
(setq package-archives '(("gnu" . "https://elpa.gnu.org/packages/")
                         ;("marmalade" . "https://marmalade-repo.org/packages/")
                         ("melpa" . "https://melpa.org/packages/")))


;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;Resize de ventanas con las teclas F;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;; Use control-arrow keys for window resizing
(global-set-key [f7] 'enlarge-window-horizontally)
(global-set-key [f8] 'shrink-window-horizontally)
(global-set-key [f9] 'enlarge-window)
(global-set-key [f10] 'shrink-window)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;Navegacion por ventanas con el cursor y escape;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(global-set-key (kbd "ESC <left>") 'windmove-left)        ; move to left window
(global-set-key (kbd "ESC <right>") 'windmove-right)      ; move to right window
(global-set-key (kbd "ESC <up>") 'windmove-up)            ; move to upper window
(global-set-key (kbd "ESC <down>") 'windmove-down)        ; move to lower window

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;; A la hora de cargar te devuelva a la misma posicion donde estabas;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(require 'saveplace)
;(setq-default save-place t)
(save-place-mode 1)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;Para ver los parentesis que corresponden;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(show-paren-mode t)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;Para ver en que columna estas;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq column-number-mode t)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;NEOTREE F12 y directorios a la izquierda;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(require 'neotree)
  (global-set-key [f12] 'neotree-toggle)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;Cambiamos la tecla meta alt a q no tenga funcion esto para MACOS;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq mac-option-modifier nil)


;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;Cambiamos la tecla meta alt a q no tenga funcion esto para MACOS;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq mac-option-modifier nil)


;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;Yasnippet;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(add-to-list 'load-path
              "~/.emacs.d/snippets")
(require 'yasnippet)
(yas-global-mode 1)


; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;Look And Feel ( Coloreado );;;;;;;;;;;;;;;;;;;;;;;;;
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; (custom-set-faces
;  ;; custom-set-faces was added by Custom.
;  ;; If you edit it by hand, you could mess it up, so be careful.
;  ;; Your init file should contain only one such instance.
;  ;; If there is more than one, they won't work right.
;  '(default ((t (:inherit nil :stipple nil :background "gray0" :foreground "green" :inverse-video nil :box nil :strike-through nil :overline nil :underline nil :slant normal weight normal :width normal :family "monospace"))))
;  '(background "black")
;  '(font-lock-builtin-face ((((class color) (background dark)) (:foreground "Turquoise"))))
;  '(font-lock-comment-face ((t (:foreground "red"))))
;  '(font-lock-constant-face ((((class color) (background dark)) (:bold t :foreground "DarkOrchid"))))
;  '(font-lock-doc-string-face ((t (:foreground "yellow"))))
;  '(font-lock-function-name-face ((t (:foreground "green1"))))
;  '(font-lock-keyword-face ((t (:foreground "DeepSkyBlue"))))
;  '(font-lock-preprocessor-face ((t (:italic nil :foreground "CornFlowerBlue"))))
;  '(font-lock-reference-face ((t (:foreground "DodgerBlue"))))
;  '(font-lock-string-face ((t (:foreground "gold2")))))

;;;;;;;;Para que aparezca coloreado cuando seleccionas un texto
(transient-mark-mode t)
;;;;;;;;;;;;;;;;;;;;;;;;Comentario en azul;
(set-face-foreground 'font-lock-comment-face "Red" )
(set-variable font-lock-comment-face 'font-lock-comment-face)

; Habilito los colores de emacs en modo dark
(setq frame-background-mode 'dark)


;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;JAVASCRIPT AND REACTJS;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;TIDE;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;; Setup-tide-mode
(defun setup-tide-mode ()
  (interactive)
  (tide-setup)
  (flycheck-mode +1)
  (setq flycheck-check-syntax-automatically '(save mode-enabled))
  (eldoc-mode +1)
  (tide-hl-identifier-mode +1)
  ;; company is an optional dependency. You have to
  ;; install it separately via package-install
  ;; `M-x package-install [ret] company`
  (company-mode +1))

;; Aligns annotation to the right hand side
(setq company-tooltip-align-annotations t)

;; Formats the buffer before saving
(add-hook 'before-save-hook 'tide-format-before-save)

(add-hook 'typescript-mode-hook #'setup-tide-mode)

;; Format options
(setq tide-format-options
      '(:insertSpaceAfterFunctionKeywordForAnonymousFunctions t
        :placeOpenBraceOnNewLineForFunctions nil))

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;RJSX;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;;;;;;;;;;;;;;;;;;;;;;; Cargar archivos .js en rjsx-mode
(add-to-list 'auto-mode-alist '("\\.js$" . rjsx-mode))

;;;;;;;;;;;;;;;;;;;;;;; Cargar archivos .tsx en rjsx-mode
(add-to-list 'auto-mode-alist '("\\.tsx\\'" . rjsx-mode))

;;;;;;;;;;;;;;;;;;;;;;;;;;Linking RJSX and TIDE;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;; Replace tab for 2 spaces identation in rjsx-mode, and invoke setup-tide-mode
(add-hook 'rjsx-mode-hook
          (lambda ()
            (setq indent-tabs-mode nil) ;;Use space instead of tab
            (setq js-indent-level 2) ;;space width is 2 (default is 4)
            (setq js2-strict-missing-semi-warning nil) ;;disable semicolon warning
            (when (string-equal "js" (file-name-extension buffer-file-name))
              (setup-tide-mode)) ;; call setup-tide-mode
            (when (string-equal "jsx" (file-name-extension buffer-file-name))
              (setup-tide-mode)) ;; call setup-tide-mode 
	    ))



(custom-set-variables
 ;; custom-set-variables was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(package-selected-packages
   (quote
    (helm-projectile ibuffer-vc xclip dired-subtree diredful dired-rainbow projectile undo-tree pdf-tools json-navigator json-mode impatient-mode markdown-mode ibuffer-sidebar sql-indent tide yasnippet web-mode rjsx-mode neotree magit flycheck company-tern auto-complete))))


;;MYSQL
(add-hook 'sql-interactive-mode-hook
          (lambda ()
            (toggle-truncate-lines t)))

(setq sql-mysql-options '("-C" "-f" "-t" "-n" "-A")) ; for windows

(setq sql-connection-alist
      '((corvus (sql-product 'mysql)
                  (sql-port 3306)
                  (sql-server "loginsmsbulk.com")
                  (sql-user "corvusalbus")
                  (sql-password "g^2W-RusF-j+tvDu")
		  (sql-database "accounts")
                 )
        ))

(defun corvus ()
  (interactive)
  (my-sql-connect 'mysql 'corvus))

(defun my-sql-connect (product connection)
  ;; remember to set the sql-product, otherwise, it will fail for the first time
  ;; you call the function
  (setq sql-product product)
  (sql-connect connection))



;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;             C           ;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;Tabulacion 4 caracteres C;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(setq-default indent-tabs-mode nil)
(setq-default tab-width 4)
(setq c-basic-offset 4)
(setq c-default-style "bsd"
      c-basic-offset 4)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;Para ver los parentesis que corresponden usando el % sobre el simbolo;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(show-paren-mode t)

(global-set-key "%" 'match-paren)
          
          (defun match-paren (arg)
            "Go to the matching paren if on a paren; otherwise insert %."
            (interactive "p")
            (cond ((looking-at "\\s(") (forward-list 1) (backward-char 1))
                  ((looking-at "\\s)") (forward-char 1) (backward-list 1))
                  (t (self-insert-command (or arg 1)))))

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;Numeros en las lineas del codigo        ;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;(global-linum-mode 1)
(add-hook 'prog-mode-hook 'linum-mode)
(setq linum-format "%3d ")

;;;;;;;;;;;;;;;Autocomplete
(require 'auto-complete)
(global-auto-complete-mode t)


;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;Compilacion;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;compilar con f5
(global-set-key [f5] 'compile)


(defun my-compilation-hook ()
  (when (not (get-buffer-window "*compilation*"))
    (save-selected-window
      (save-excursion
        (let* ((w (split-window-vertically))
               (h (window-height w)))
          (select-window w)
          (switch-to-buffer "*compilation*")
          (shrink-window (- h 10)))))))
(add-hook 'compilation-mode-hook 'my-compilation-hook)

;; auto scroll to the end 
(setq compilation-scroll-output 1)
(setq column-number-mode t)


(global-flycheck-mode)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;MARKDOWN;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

(defun markdown-html (buffer)
  (princ (with-current-buffer buffer
    (format "<!DOCTYPE html><html><title>Impatient Markdown</title><xmp theme=\"united\" style=\"display:none;\"> %s  </xmp><script src=\"http://strapdownjs.com/v/0.2/strapdown.js\"></script></html>" (buffer-substring-no-properties (point-min) (point-max))))
  (current-buffer)))
(put 'downcase-region 'disabled nil)
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;


;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;; HL-LINE;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;; SOmbreado de la linea actual ;;;;;;;;;;;;;;;;;;;
(require 'hl-line)
(set-face-background hl-line-face "gray13")
;Habilito hl-line mode global
(global-hl-line-mode 1)
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;DIRED ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;; DIREDFUL: colores;;;;;;;;
(diredful-mode 1)
(add-hook 'dired-mode-hook
      (lambda ()
        (dired-hide-details-mode)
        ))
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;Anidar en dired mode el abrir un subdirectorio
(define-key dired-mode-map "i" 'dired-subtree-insert)
(define-key dired-mode-map ";" 'dired-subtree-remove)
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;


;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;; IDO ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;autocompletar en la seleccion del algun menu;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

(ido-mode 1)
;(setq ido-separator "\n")
;; Para evitar cuando quiero abrir el DIRED mode desde la apertura de archivos
(setq ido-show-dot-for-dired t)
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;; XCLIP ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;; para copiar y pegar entre emacs text y el entorno de ventanas ;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;Habilito xclip-mode global
(xclip-mode 1)
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;IBUFFER;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;; Para que abra el ibuffer en vez del buffer-menu
(global-set-key (kbd "C-x C-b") 'ibuffer)
(global-set-key (kbd "C-q") 'ibuffer)

;; Sub grupos de ibuffer
;; COmentado pq projectile reorganizara

; (setq ibuffer-saved-filter-groups
;           (quote (("default"
;                    ("dired" (mode . dired-mode))
;                    ;("perl" (mode . cperl-mode))
;                    ("JS" (mode . rjsx-mode))
;                    ;("erc" (mode . erc-mode))
;                    ;("planner" (or
;                    ;            (name . "^\\*Calendar\\*$")
;                    ;            (name . "^diary$")
;                    ;            (mode . muse-mode)))
;                    ("emacs" (or
;                              (name . "^\\*scratch\\*$")
;                              (name . "^\\*Messages\\*$")))
;                    ("gnus" (or
;                             (mode . message-mode)
;                             (mode . bbdb-mode)
;                             (mode . mail-mode)
;                             (mode . gnus-group-mode)
;                             (mode . gnus-summary-mode)
;                             (mode . gnus-article-mode)
;                             (name . "^\\.bbdb$")
;                             (name . "^\\.newsrc-dribble")))))))
; 
; 
; (add-hook 'ibuffer-mode-hook
;               (lambda ()
;                 (ibuffer-switch-to-saved-filter-groups "default")))

;;Automatic refresh ibuffer
(add-hook 'ibuffer-mode-hook (lambda () (ibuffer-auto-mode 1)))



;; Use human readable Size column instead of original one
(require 'ibuffer )
(define-ibuffer-column size-h
  (:name "Size" :inline t)
  (cond
   ((> (buffer-size) 1000000) (format "%7.1fM" (/ (buffer-size) 1000000.0)))
   ((> (buffer-size) 100000) (format "%7.0fk" (/ (buffer-size) 1000.0)))
   ((> (buffer-size) 1000) (format "%7.1fk" (/ (buffer-size) 1000.0)))
   (t (format "%8d" (buffer-size)))))

;; Modify the default ibuffer-formats
(setq ibuffer-formats
      '((mark modified read-only " "
              (name 18 18 :left :elide)
              " "
              (size-h 9 -1 :right)
              " "
              (mode 16 16 :left :elide)
              " "
              filename-and-process)))









;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;; PROJECTILE ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

(projectile-global-mode)


;; PROJECTILE-IBUFFER integration
;; Define ibuffer filter groups for each known project
(defun my/define-projectile-filter-groups ()
  (when (boundp 'projectile-known-projects)
    (setq my/project-filter-groups
          (mapcar
           (lambda (it)
             (let ((name (file-name-nondirectory (directory-file-name it))))
               `(,name (filename . ,(expand-file-name it)))))
           projectile-known-projects))))

;; Set up default ibuffer filter groups
(setq ibuffer-saved-filter-groups
      (list
       (cons "default"
             (append
              (my/define-projectile-filter-groups)
              ;; ... whatever other groups you want, e.g.
              '(("dired" (mode . dired-mode))
                ("erc" (mode . erc-mode)))
              ))))

;; Enable default groups by default
(add-hook 'ibuffer-mode-hook
          (lambda ()
            (ibuffer-switch-to-saved-filter-groups "default")))

;; You probably don't want to see empty project groups
(setq ibuffer-show-empty-filter-groups nil)





;; Crear el sort por path filename  s p para ordenar por nombre y ruta completa
(define-ibuffer-sorter filename-or-dired
  "Sort the buffers by their pathname."
  (:description "filenames plus dired")
  (string-lessp
   (with-current-buffer (car a)
     (or buffer-file-name
         (if (eq major-mode 'dired-mode)
             (expand-file-name dired-directory))
         ;; so that all non pathnames are at the end
         "~"))
   (with-current-buffer (car b)
     (or buffer-file-name
         (if (eq major-mode 'dired-mode)
             (expand-file-name dired-directory))
         ;; so that all non pathnames are at the end
         "~"))))
    (define-key ibuffer-mode-map (kbd "s p")     'ibuffer-do-sort-by-filename-or-dired)



(set (make-local-variable 'ibuffer-sorting-mode)
     ibuffer-default-sorting-mode)

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;; E-SHELL ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;;;;;;;;; Completition like bash

(add-hook
 'eshell-mode-hook
 (lambda ()
      (setq pcomplete-cycle-completions nil)))

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
```