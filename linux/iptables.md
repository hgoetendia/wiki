---
title: Iptables
description: 
published: true
date: 2020-05-23T23:22:15.211Z
tags: 
---

# Show rules

## List Rules by Specification

```sh
sudo iptables -S
```

## List specific chain
```sh
sudo iptables -S TCP
```
## List rules as tables
```sh
sudo iptables -L
```
```sh
sudo iptables -L INPUT
```

## List NAT rules


```text
[root@server ]# iptables -t nat -L --line-numbers
Chain PREROUTING (policy ACCEPT)
num  target     prot opt source               destination         

Chain INPUT (policy ACCEPT)
num  target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
num  target     prot opt source               destination         


Chain POSTROUTING (policy ACCEPT)
num  target     prot opt source               destination         
1    SNAT       all  --  anywhere             anywhere             to:110.33.255.132
```


## Remove iptables POSTROUTING NAT rule


```text
[root@server ]# iptables -t nat -D POSTROUTING 1

```




# Block IP / Unblock
## Block
```text
iptables -A INPUT -s 209.175.453.23 -j DROP
```
## Unblock
```text
iptables -D INPUT -s 209.175.453.23 -j DROP
```

# Block IP and destination and TCP port
```text
iptables -A INPUT -s 209.175.453.23 -p tcp --destination-port 22 -j DROP
```