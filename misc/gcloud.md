---
title: Gcloud
description: A quick summary of Gcloud
published: true
date: 2019-10-28T00:42:56.056Z
tags: 
---

Error:

```text
"ServiceException: 401 Anonymous caller does not have storage.objects.create access to ....."
```
Solution:

```sh
gcloud auth  activate-service-account   --key-file=my.json
```
