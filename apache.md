---
title: Apache
description: Web server
published: true
date: 2020-04-26T17:57:18.552Z
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