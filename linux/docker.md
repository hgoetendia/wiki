---
title: Docker
description: All containers are run by a single operating system kernel and therefore use fewer resources than virtual machines.
published: true
date: 2020-05-30T20:07:06.090Z
tags: docker, container
---

Docker has two parts, one daemon and a client, we will work in console with Docker client.

# Docker daemon 

## Installing
```
sudo apt-get install docker.io
```

## Starting
```
sudo systemctl start docker
```

Checking version
```
$ sudo docker version
Client:
 Version:           19.03.6
 API version:       1.40
 Go version:        go1.12.10
 Git commit:        369ce74a3c
 Built:             Fri Feb 28 23:26:00 2020
 OS/Arch:           linux/amd64
 Experimental:      false

Server:
 Engine:
  Version:          19.03.6
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.12.10
  Git commit:       369ce74a3c
  Built:            Wed Feb 19 01:04:38 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.3.3-0ubuntu1~19.10.2
  GitCommit:        
 runc:
  Version:          spec: 1.0.1-dev
  GitCommit:        
 docker-init:
  Version:          0.18.0
  GitCommit:        

```

```
$ sudo docker info
Client:
 Debug Mode: false

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 19.03.6
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 
 runc version: 
 init version: 
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 5.3.0-55-generic
 Operating System: Ubuntu 19.10
 OSType: linux
 Architecture: x86_64
 CPUs: 8
 Total Memory: 15.55GiB
 Name: XXXXXXXX
 ID: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false

WARNING: No swap limit support
```


Searching online an OS image


```
$ sudo docker search debian
NAME                                               DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
ubuntu                                             Ubuntu is a Debian-based Linux operating sys…   10946               [OK]                
debian                                             Debian is a Linux distribution that's compos…   3497                [OK]                
arm32v7/debian                                     Debian is a Linux distribution that's compos…   66                                      
itscaro/debian-ssh                                 debian:jessie                                   28                                      [OK]
arm64v8/debian                                     Debian is a Linux distribution that's compos…   23                                      
samueldebruyn/debian-git                           a minimal docker container with debian and g…   22                                      [OK]
multiarch/debian-debootstrap                       multiarch ports of debian-debootstrap           12                                      
i386/debian                                        Debian is a Linux distribution that's compos…   10                                      
eboraas/debian                                     Debian base images, for all currently-availa…   8                                       [OK]
.
.

```

```
$ sudo docker search centos
NAME                               DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
centos                             The official build of CentOS.                   6018                [OK]                
ansible/centos7-ansible            Ansible on Centos7                              129                                     [OK]
consol/centos-xfce-vnc             Centos container with "headless" VNC session…   115                                     [OK]
jdeathe/centos-ssh                 OpenSSH / Supervisor / EPEL/IUS/SCL Repos - …   114                                     [OK]
centos/mysql-57-centos7            MySQL 5.7 SQL database server                   76                                      
imagine10255/centos6-lnmp-php56    centos6-lnmp-php56                              58                                      [OK]
tutum/centos                       Simple CentOS docker image with SSH access      46                                      
centos/postgresql-96-centos7       PostgreSQL is an advanced Object-Relational …   44                                      
.
.
```
```
$ sudo docker search busybox 
NAME                      DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
busybox                   Busybox base image.                             1906                [OK]                
progrium/busybox                                                          71                                      [OK]
radial/busyboxplus        Full-chain, Internet enabled, busybox made f…   30                                      [OK]
arm32v7/busybox           Busybox base image.                             8                                       
.
.
```

# Setting an OS
```
$ sudo docker pull busybox 
Using default tag: latest
latest: Pulling from library/busybox
d9cbbca60e5f: Pull complete 
Digest: sha256:836945da1f3afe2cfff376d379852bbb82e0237cb2925d53a13f53d6e8a8c48c
Status: Downloaded newer image for busybox:latest
docker.io/library/busybox:latest
```
```
$ sudo docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
busybox             latest              78096d0a5478        2 weeks ago         1.22MB
```


# Running container
```
$ sudo docker run -it busybox sh
/ # ls
bin   dev   etc   home  proc  root  sys   tmp   usr   var
/ # pwd
/
/ # 
```


Checking if container is working:

```
$ sudo docker ps -a 
[sudo] password for horacio: 
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
4374d269edae        busybox             "sh"                42 minutes ago      Up 42 minutes                           laughing_heisenberg
```

If you are running a second container the output will be:
```
$ sudo docker ps -a 
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
8689364950a8        busybox             "sh"                20 seconds ago      Up 18 seconds                           nostalgic_williamson
4374d269edae        busybox             "sh"                44 minutes ago      Up 44 minutes                           laughing_heisenberg
```

# Command list

Searching an image:
```
sudo docker search debian
```

Downloading an image:
```
sudo docker pull debian
```

Runing container from an image:

```
sudo docker run -it debian bash
```

Check containers / status / info:

```
sudo docker ps -a
```

A stoped container , previously created ( STATUS Exited ), can be started with docker start):

```
sudo docker start ID (or name)
```

Entering in a container:
```
sudo docker attach ID (or name)
```

Stoping a container:
```
sudo docker stop ID (o nombre)
```
Removing a container:
```
sudo docker rm ID (o nombre)
```


Save an new image  from a modified container:
```
sudo docker commit -m “my coment” -a myAuthor ID myNewName
```