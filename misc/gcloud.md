---
title: Gcloud
description: A quick summary of Gcloud
published: true
date: 2020-03-19T00:07:13.221Z
tags: 
---

# Install google tools API



```sh
python3.7 -m venv my-bqloads
source my-bqloads/bin/activate
pip3.7 install wheel
pip3.7 install google-cloud
pip3.7 install google-cloud-bigquery
```

Error:

```text
"ServiceException: 401 Anonymous caller does not have storage.objects.create access to ....."
```
Solution:

```sh
gcloud auth  activate-service-account   --key-file=my.json
```
