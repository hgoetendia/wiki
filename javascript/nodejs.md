---
title: Nodejs
description: 
published: true
date: 2020-05-05T02:37:41.529Z
tags: 
---

# Install 
This will install node and npm.
## From sources


```sh
sudo yum install gcc gcc-c++ wget
wget http://nodejs.org/dist/latest-v10.x/node-v10.14.2.tar.gz
tar xvf node-v10.14.2.tar.gz
cd node-v10.14.2
./configure
make
sudo make install
```

## From the EPEL Repository 

Tested in Centos


```sh
sudo yum install epel-release
sudo yum install nodejs
node --version
```

## From NodeSource
As root execute (tested in Centos):

```sh
curl -sL https://rpm.nodesource.com/setup_11.x | bash -
sudo yum install -y nodejs
```



## Error: ENOSPC: System limit for number of file watchers reached

Add in `/etc/sysctl.conf`


```text
fs.inotify.max_user_watches = 524288
```

Then 
```sh
sysctl -p
```

to read the new setting.


# Start a project

## Initialize
 -y/--yes to skip the questionnaire altogether.

```
$ npm init -y

Wrote to /home/XXX/XXX/XX/XXXX/package.json:      
                                                           
{                                                          
  "name": "XXXX",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}                                                          
```
## Handle sessions

-D, --save-dev : package will apear in devDependencies 

```
npm i express express-session
npm i -D nodemon standard
```

app.js

```js
const express = require('express')
const session = require('express-session')

const {
  PORT = 3000
} = process.env

const app = express()

app.listen(PORT, () => console.log(`http://localhost:${PORT}`))
```

packages.json

Change line 7 from `test` to `dev` and `nodemon app`

```json
{
  "name": "jarlok",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
  "dev": "nodemon app"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1",
    "express-session": "^1.17.1"
  },
  "devDependencies": {
    "nodemon": "^2.0.3",
    "standard": "^14.3.3"
  }
}
```
Starting

```sh
[mycompu]$ npm run dev

> jarlok@1.0.0 dev /home/XXX/XXX/XXX/XXX
> nodemon app

[nodemon] 2.0.3
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,mjs,json
[nodemon] starting `node app.js`
http://localhost:3000
```

Update app.js based in `express-session` documentation

https://www.npmjs.com/package/express-session
```js
var app = express()
app.set('trust proxy', 1) // trust first proxy
app.use(session({
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: true,
  cookie: { secure: true }
}))
```

app.js
{"gitdown": "gist", "id": "d3e4212c799252bac5fa"}
{% gist 123456789 %}

<script src="https://gist.github.com/hgoetendia/f1de538507e8efee16ae5291436c1941.js"></script>

