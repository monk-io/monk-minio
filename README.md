# Minio & Monk

This repository contains Monk.io template to deploy Minio Cluster either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

## Prerequisites

- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

## Make sure monkd is running

```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository

```bash
git clone git@github.com:monk-io/monk-minio.git
```

## Load Template

```bash
cd monk-minio
monk load MANIFEST
```

```bash
foo@bar:~$ monk list monk-minio
✔ Got the list
Type      Template     Repository  Version  Tags
runnable  minio/base   local       -        Object storage, Cloud storage, Distributed storage, S3 compatible, Open source, Data management, File sharing, Backup and recovery, High availability
runnable  minio/minio  local       -        Object storage, Cloud storage, Distributed storage, S3 compatible, Open source, Data management, File sharing, Backup and recovery, High availability
```

## Deploy Stack

```bash
foo@bar:~$ monk run minio/minio
✔ Starting the run job: local/minio/minio... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ New container 3cecf5dddbe0c8b614e98f2c3a1aae09-local-minio-minio-minio created DONE
✔ Started local/minio/minio
🔩 templates/local/minio/minio
 └─🧊 Peer local
    └─🔩 templates/local/minio/minio
       └─📦 3cecf5dddbe0c8b614e98f2c3a1aae09-local-minio-minio-minio running
          ├─🧩 minio/minio:latest
          └─💾 /var/lib/monkd/volumes/monk-minio -> /data

💡 You can inspect and manage your above stack with these commands:
        monk logs (-f) local/minio/minio - Inspect logs
        monk shell     local/minio/minio - Connect to the container's shell
        monk do        local/minio/minio/action_name - Run defined action (if exists)
💡 Check monk help for more!
```

## Access Console

[http://monk:9001/](http://monk:9001/)

## Variables

The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable             | Description  | Default       |
| -------------------- | ------------ | ------------- |
| minio_admin_username | Username     | administrator |
| minio_admin_password | Password     | administrator |
| console_port         | Console Port | 9001          |

## Stop| remove and clean up workloads and templates

```bash
monk purge -x -a
```
