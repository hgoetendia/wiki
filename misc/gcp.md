---
title: Google cloud platform GCP
description: GCP
published: true
date: 2020-03-10T14:03:04.633Z
tags: 
---

# Cheat sheet

## Copy to bucket

```bash
gsutil cp foo.txt  gs://my-bucket/path/to/target/
```

## SSH to cloud shell from any terminal.

```
erik@localhost:~$ ls
Desktop
erik@localhost:~$ gcloud alpha cloud-shell ssh
Welcome to Cloud Shell! Type "help" to get started.
erik@cloudshell:~$ ls
server.py  README-cloudshell.txt
```

## Copy files between your Cloud Shell and your local machine

```
erik@localhost:~$ gcloud alpha cloud-shell scp cloudshell:~/data.txt localhost:~
data.txt                                           100% 1897    28.6KB/s   00:00
erik@localhost:~$
```

## Mount your Cloud Shell home directory onto your local file system

It needs sshfs installed. This allows you to edit the files in your Cloud Shell home directory using whatever local tools you want! All the data in your remotely mounted file system is stored on a Persistent Disk, so it's fast, strongly consistent and retained across sessions and regions.

```
erik@localhost:~$ gcloud alpha cloud-shell get-mount-command ~/my-cloud-shell
sshfs ekuefler@35.197.73.198: /home/ekuefler/my-cloud-shell -p 6000 -oIdentityFile=/home/ekuefler/.ssh/google_compute_engine
erik@localhost:~$ sshfs ekuefler@35.197.73.198: /home/ekuefler/my-cloud-shell -p 6000 -oIdentityFile=/home/ekuefler/.ssh/google_compute_engine
erik@localhost:~$ cd my-cloud-shell
erik@localhost:~$ ls
server.py  README-cloudshell.txt
erik@localhost:~$ vscode server.py
```

# Big Query (BQ)

## Drop column

```sql
CREATE OR REPLACE TABLE `XXXX.yyy.myTable` AS
SELECT
  * EXCEPT ( myColumn1, myColumn2 )
FROM
  `XXXX.yyy.myTable`
```

## Change column type

Change column b to an FLOAT

```sql
CREATE OR REPLACE TABLE `transactions.test_table` AS
SELECT
  * EXCEPT (b),
  CAST(b AS FLOAT64) AS b
FROM
  `transactions.test_table`;
```

## Load (append) data to big query

```sql
bq --project myProject load --source_format=CSV --noreplace --field_delimiter='|' --skip_leading_rows 1 myDataset.myTable gs://XXXX/XXXXX/XXXX.csv.gz
```