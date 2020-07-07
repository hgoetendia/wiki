---
title: Nginx, create basic authentication
description: 
published: true
date: 2020-07-07T03:54:10.476Z
tags: authentication, basic authentication, htpasswd
---

# Basic authentication in NGINX and APACHE
Modify your webserver config file:

NGINX

```
server {
        listen 80;
        server_name xym.sytes.net;
        auth_basic    "Admin-Section";
        auth_basic_user_file /etc/nginx/htpasswdxym;

        root /var/www/;

        location /xymon/ {
                alias /var/www/xymon/;
                index index.html ;
        }

        location /xymon-cgi/ {
                fastcgi_pass  unix:/var/run/fcgiwrap.socket;
                # Fastcgi parameters, include the standard ones
                include /etc/nginx/fastcgi_params;
                # Adjust non standard parameters (SCRIPT_FILENAME)
                fastcgi_param SCRIPT_FILENAME  /usr/share/xymon/cgi-bin$fastcgi_script_name;
                #fastcgi_param DOCUMENT_ROOT /usr/share/xymon/cgi-bin/;
                fastcgi_param SCRIPT_NAME $fastcgi_script_name;

                #include /etc/nginx/fastcgi_params;

        }

        location /cgi-secure/ {

                        alias /usr/share/xymon/cgi-secure/ ;
        }
}
```

APACHE

```bash
Alias /xymon  "/var/www/xymon"
<Directory "/var/www/xymon">
    Options Indexes FollowSymLinks Includes MultiViews
    <IfModule mod_authz_core.c>
        # Apache 2.4+
        #Require all granted   #Esto quite
    </IfModule>
    <IfModule !mod_authz_core.c>
        Order deny,allow
        Allow from all
    </IfModule>
##anadi
    AuthUserFile /etc/xymon/xymonpasswd
    AuthGroupFile /etc/xymon/xymongroups
    AuthType Basic
    AuthName "Xymon Administration"

    # "valid-user" restricts access to anyone who is logged in.
    Require valid-user

    # "group admins" restricts access to users who have logged in, AND
    # are members of the "admins" group in xymongroups.
    # Require group admins
##
</Directory>
```

Execute this command.


```
htpasswd -c /etc/nginx/htpasswdxym monitoreo
```