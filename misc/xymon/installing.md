---
title: Installing Xymon
description: 
published: true
date: 2020-07-07T02:44:47.620Z
tags: xymon, bb, xymon install
---


# Centos With NGINX

# Requirements
```
yum install nginx
yum install xymon
yum install xymon-client
yum install fcgiwrap
yum install spawn-fcgi

```


# NGINX config

```
server {
        listen 80;
        server_name xym.sytes.net;
        #auth_basic    "Admin-Section";
        #auth_basic_user_file /etc/nginx/.htpasswd;

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


# Fastcgi

`/etc/nginx/fastcgi_params`

```
fastcgi_param  QUERY_STRING       $query_string;
fastcgi_param  REQUEST_METHOD     $request_method;
fastcgi_param  CONTENT_TYPE       $content_type;
fastcgi_param  CONTENT_LENGTH     $content_length;

fastcgi_param  SCRIPT_NAME        $fastcgi_script_name;
fastcgi_param  REQUEST_URI        $request_uri;
fastcgi_param  DOCUMENT_URI       $document_uri;
fastcgi_param  DOCUMENT_ROOT      $document_root;
fastcgi_param  SERVER_PROTOCOL    $server_protocol;
fastcgi_param  REQUEST_SCHEME     $scheme;
fastcgi_param  HTTPS              $https if_not_empty;

fastcgi_param  GATEWAY_INTERFACE  CGI/1.1;
fastcgi_param  SERVER_SOFTWARE    nginx/$nginx_version;

fastcgi_param  REMOTE_ADDR        $remote_addr;
fastcgi_param  REMOTE_PORT        $remote_port;
fastcgi_param  SERVER_ADDR        $server_addr;
fastcgi_param  SERVER_PORT        $server_port;
fastcgi_param  SERVER_NAME        $server_name;

# PHP only, required if PHP was built with --enable-force-cgi-redirect
fastcgi_param  REDIRECT_STATUS    200;
```

# spawn-fcgi
`cat /etc/sysconfig/spawn-fcgi`

The "-f" in the final is to log in NGINX

```
# You must set some working options before the "spawn-fcgi" service will work.
# If SOCKET points to a file, then this file is cleaned up by the init script.
#
# See spawn-fcgi(1) for all possible options.
#
# Example :
#SOCKET=/var/run/php-fcgi.sock
#OPTIONS="-u apache -g apache -s $SOCKET -S -M 0600 -C 32 -F 1 -P /var/run/spawn-fcgi.pid -- /usr/bin/php-cgi"


# You must set some working options before the "spawn-fcgi" service will work.
# If SOCKET points to a file, then this file is cleaned up by the init script.
#
# See spawn-fcgi(1) for all possible options.
#
# Example :
#SOCKET=/var/run/php-fcgi.sock
#OPTIONS="-u apache -g apache -s $SOCKET -S -M 0600 -C 32 -F 1 -P /var/run/spawn-fcgi.pid -- /usr/bin/php-cgi"
FCGI_SOCKET=/var/run/fcgiwrap.socket
FCGI_PROGRAM=/usr/sbin/fcgiwrap
FCGI_USER=nginx
FCGI_GROUP=nginx
FCGI_EXTRA_OPTIONS="-M 0700"
OPTIONS="-u $FCGI_USER -g $FCGI_GROUP -s $FCGI_SOCKET -S $FCGI_EXTRA_OPTIONS -F 1 -P /var/run/spawn-fcgi.pid -- $FCGI_PROGRAM -f"
```


# Xymon files

`tree /var/www/xymon/`
 
```
/var/www/xymon/
├── critical.html
├── gifs -> /usr/share/xymon/server/static/gifs
├── index.html -> xymon.html
├── menu -> /usr/share/xymon/server/static/menu
├── nongreen.html
├── red.html
└── xymon.html

2 directories, 5 files
```

`tree /usr/share/xymon`

```
.
├── bin -> /usr/libexec/xymon
├── certs -> /etc/xymon/certs
├── cgi-bin
│   └── xymon-cgi
│       ├── acknowledgements.sh
│       ├── appfeed-critical.sh
│       ├── appfeed.sh
│       ├── certreport.sh
│       ├── columndoc.sh
│       ├── confreport-critical.sh
│       ├── confreport.sh
│       ├── criticalview.sh
│       ├── csvinfo.sh
│       ├── datepage.sh
│       ├── eventlog.sh
│       ├── findhost.sh
│       ├── ghostlist.sh
│       ├── historylog.sh
│       ├── history.sh
│       ├── hostgraphs.sh
│       ├── hostlist.sh
│       ├── nongreen.sh
│       ├── notifications.sh
│       ├── perfdata.sh
│       ├── reportlog.sh
│       ├── report.sh
│       ├── showgraph.sh
│       ├── snapshot.sh
│       ├── svcstatus.sh
│       └── topchanges.sh
├── cgi-secure
│   ├── ackinfo.sh
│   ├── acknowledge.sh
│   ├── chpasswd.sh
│   ├── criticaleditor.sh
│   ├── enadis.sh
│   └── useradm.sh
├── client -> /usr/share/xymon-client
├── etc -> /etc/xymon
├── ext -> /etc/xymon/ext
├── server -> /usr/share/xymon
├── static
│   ├── gifs
│   │   ├── arrow.gif
│   │   └── zoom.gif
│   ├── help
│   │   ├── about.html
│   │   ├── bb-to-xymon.html
│   │   ├── clonewarn.jpg
│   │   ├── configure.txt
│   │   ├── criticalsystems.html
│   │   ├── critview-detail-acked.jpg
│   │   ├── mainview.jpg
│   │   ├── manpages
│   │   │   ├── index.html
│   │   │   ├── man1
│   │   │   │   ├── ackinfo.cgi.1.html
│   │   │   │   ├── acknowledge.cgi.1.html
│   │   │   │   ├── appfeed.cgi.1.html
│   │   │   │   ├── clientupdate.1.html
│   │   │   │   ├── combostatus.1.html
│   │   │   │   ├── confreport.cgi.1.html
│   │   │   │   ├── criticaleditor.cgi.1.html
│   │   │   │   ├── criticalview.cgi.1.html
│   │   │   │   ├── csvinfo.cgi.1.html
│   │   │   │   ├── datepage.cgi.1.html
│   │   │   │   ├── eventlog.cgi.1.html
│   │   │   │   ├── findhost.cgi.1.html
│   │   │   │   ├── ghostlist.cgi.1.html
│   │   │   │   ├── history.cgi.1.html
│   │   │   │   ├── hostgraphs.cgi.1.html
│   │   │   │   ├── logfetch.1.html
│   │   │   │   ├── orcaxymon.1.html`
│   │   │   │   ├── report.cgi.1.html
│   │   │   │   ├── reportlog.cgi.1.html
│   │   │   │   ├── showgraph.cgi.1.html
│   │   │   │   ├── snapshot.cgi.1.html
│   │   │   │   ├── statusreport.cgi.1.html
│   │   │   │   ├── svcstatus.cgi.1.html
│   │   │   │   ├── xymon.1.html
│   │   │   │   ├── xymoncfg.1.html
│   │   │   │   ├── xymoncmd.1.html
│   │   │   │   ├── xymondigest.1.html
│   │   │   │   ├── xymongen.1.html
│   │   │   │   ├── xymongrep.1.html
│   │   │   │   ├── xymonnet.1.html
│   │   │   │   ├── xymonnet-again.sh.1.html
│   │   │   │   ├── xymonpage.cgi.1.html
│   │   │   │   └── xymonping.1.html
│   │   │   ├── man5
│   │   │   │   ├── alerts.cfg.5.html
│   │   │   ├── man7
│   │   │   │   └── xymon.7.html
│   │   │   └── man8
│   │   │       ├── enadis.cgi.8.html
│   │   ├── Renaming-430.txt
│   │   ├── stdview-detail-acked.jpg
│   │   ├── upgrade-to-430.txt
│   │   ├── xymon-alerts.html
│   │   ├── xymon-apacheconf.txt
│   │   ├── xymon-clients.png
│   │   ├── xymon-config.html
│   │   ├── xymon-hosts.png
│   │   ├── xymonmain.png
│   │   ├── xymon-mrtg.html
│   │   ├── xymonprocs.png
│   │   └── xymon-tips.html
│   └── menu
│       ├── b2t-blue.gif
│       ├── b2t-grey.gif
│       ├── t2b-blue.gif
│       ├── t2b-grey.gif
│       ├── xymonmenu-blue.css
│       └── xymonmenu-grey.css
├── web -> /etc/xymon/web
└── www -> /var/www/xymon

20 directories, 180 files
```


# Starting services:
```
systemctl restart spawn-fcgi
systemctl restart nginx
systemctl restart xymon
```

