---
title: Airflow
description: 
published: true
date: 2020-01-08T22:35:15.346Z
tags: 
---

# Installing

Ref: https://airflow.apache.org/docs/stable/installation.html

## In Debian 10

```sh
sudo apt-get install python3-pip
sudo pip install apache-airflow

# initialize the database
airflow initdb

# start the web server, default port is 8080
airflow webserver -p 8080

# start the scheduler
airflow scheduler

# visit localhost:8080 in the browser and enable the example dag in the home page

```

# Launching