---
title: Airflow
description: 
published: true
date: 2020-01-09T00:34:36.196Z
tags: 
---

# Installing & Launching

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

# Checking

```sh
http://localhost:8080
```

# Deploying and iplementing

Check `airflow.cfg` and create or check `dags_folder` for example  `/home/myuser/airflow/dags`





