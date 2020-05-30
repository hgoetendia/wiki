---
title: Markdown and live mode
description: 
published: true
date: 2020-05-30T23:43:18.838Z
tags: markdown, emacs, impatient, impatient-mode, http-start
---

# Markdown live


The pure-Emacs (nearly) solution and easy one, requiring no extra library from Python or Nodejs, is impatient-mode.

## Impatient-mode

It's designed to work with html but the doc gives a trick to make it work with markdown. It also works like a charm but requires one configuration step:

Install impatient-mode with


```
M-x package-install RET impatient-mode RET
```


given you have configured package.el to use the melpa repository.
Start an emacs' web server with:

```
M-x httpd-start.
```

Start impatient mode in the buffers you're interested to live preview: M-x impatient-mode.
Open your browser to:

```
localhost:8080/imp. 
```

You'll see the list of buffers with the mode enabled. Click on one: you see live rendering of the buffer.
To enable markdown conversion, we follow wikemacs:

Define this elisp function somewhere, like in your init file:
```
(defun markdown-html (buffer)
  (princ (with-current-buffer buffer
    (format "<!DOCTYPE html><html><title>Impatient Markdown</title><xmp theme=\"united\" style=\"display:none;\"> %s  </xmp><script src=\"http://strapdownjs.com/v/0.2/strapdown.js\"></script></html>" (buffer-substring-no-properties (point-min) (point-max))))
  (current-buffer)))
```

Tell impatient mode to use it: 
```
M-x imp-set-user-filter RET 
markdown-html RET.
```

Go back to your browser, it works!