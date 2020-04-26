---
title: Apache
description: Web server
published: true
date: 2020-04-26T18:40:38.934Z
tags: http, httpd, apache
---

# Let's encrypt
```
yum install mod_ssl
```

/etc/httpd/conf.d/test-site.conf

```
cat test-site.conf 
<VirtualHost *:8080>
    ServerAdmin admin@test.com
    DocumentRoot "/var/www/html"
    ServerName thehappymoon.com
    ServerAlias thehappymoon.com
    ErrorLog "/var/log/httpd/test.error_log"
    CustomLog "/var/log/httpd/test.access_log" common
    SSLEngine on
    SSLCertificateFile    /etc/letsencrypt/myweb.com_ecc/fullchain.cer
    SSLCertificateKeyFile  /etc/letsencrypt/myweb.com_ecc/thehappymoon.com.key
</VirtualHost>
```


# AH00132: file permissions deny server access: /var/www/html/index.html

Try check the existing permissions on the file:
```
ls -l index.html
```
Fix them if necessary:
```
chmod 644 index.html
```

If all the standard permissions are correct and you still get a Permission Denied error, you should check for extended-permissions. For example you can use the command setenforce 0 to turn off SELinux and check to see if the problem goes away. If so, ls -alZ can be used to view SELinux permission and chcon to fix them.

Eg:
```
sudo chcon -R -v -t httpd_sys_rw_content_t index.html
```