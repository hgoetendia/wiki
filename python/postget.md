---
title: Pos get
description: A quick summary of Postget
published: true
date: 2019-10-28T00:47:06.953Z
tags: 
---

# POS JSON


```python
import requests

SERVER_IP   = "127.0.0.1"
SERVER_PORT = 9090

LOCAL_PORT  = 3001
LOCAL_IP = "127.0.0.1"

url = 'http://'+ SERVER_IP +':'+str(SERVER_PORT)

params ={
    "protocol":{        
        "dateTimeSent":"2019-03-22 18:05:37.558244",
        "tentakelId": 1,        
        "comm": {
            "commandId": 1,
            "sessionId": 1,            
            "commOn": {                
                "location": "http://" + LOCAL_IP + ":" + str(LOCAL_PORT)
            }
        }
    }
}

print params

resp = requests.post(url=url, json=params)
data = resp.json()

print data

```


