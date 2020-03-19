---
title: Gcloud
description: A quick summary of Gcloud
published: true
date: 2020-03-19T00:07:16.208Z
tags: 
---

# Install google cloud tools SDK
```sh
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
sudo apt-get install apt-transport-https ca-certificates gnupg
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
sudo apt-get update && sudo apt-get install google-cloud-sdk
gcloud init
```



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
