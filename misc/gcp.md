---
title: Google cloud platform GCP
description: GCP
published: true
date: 2020-01-29T15:55:05.271Z
tags: 
---

# Header
## Copy to bucket

```bash
gsutil cp foo.txt  gs://my-bucket/path/to/target/
```

## SSH to cloud shell from any terminal.

```bash
erik@localhost:~$ ls
Desktop
erik@localhost:~$ gcloud alpha cloud-shell ssh
Welcome to Cloud Shell! Type "help" to get started.
erik@cloudshell:~$ ls
server.py  README-cloudshell.txt```