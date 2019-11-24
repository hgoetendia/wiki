---
title: RRDTool
description: RRDtool is the OpenSource industry standard, high performance data logging and graphing system for time series data. RRDtool can be easily integrated in shell scripts, perl, python, ruby, lua or tcl applications.
published: true
date: 2019-11-24T18:21:33.176Z
tags: 
---

# Create data	


```bash
### change to the script directory
$ rrdtool create data/mensajes_peru_db.rrd \
--step 300 \
DS:Enviados:GAUGE:600:0:10000000000000 \
DS:Pendientes:GAUGE:600:0:10000000000000 \
DS:Aceptados:GAUGE:600:0:10000000000000 \
DS:Fallidos:GAUGE:600:0:10000000000000 \
RRA:MAX:0.5:1:1500```