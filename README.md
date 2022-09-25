# Minio & Monk
This repository contains Monk.io template to deploy Minio Cluster either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

# Prerequisites
- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

#### Make sure monkd is running.
```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository
```bash
git clone https://github.com/Burakhan/monk-minio
```

## Load Template
```bash
cd monk-minio
monk load MANIFEST
```


#### Let's take a look at the themes I have installed.
```bash
foo@bar:~$ monk list monk-minio
✔ Got the list
Type      Template          Repository  Version  Tags
runnable  monk-minio/minio1 local       -        -
runnable  monk-minio/minio1 local       -        -
runnable  monk-minio/nginx  local       -        -
runnable  monk-minio/stack  local       -        -

```

## Deploy Stack
```bash
foo@bar:~$ monk run monk-minio/stack
? Select tag to run [local/monk-minio/stack] on: monk
✔ Starting the job: local/monk-minio/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% docker.io/bitnami/nginx:latest minio-2
✔ [================================================] 100% quay.io/minio/minio:RELEASE.2022-09-17T00-09-45Z minio-1
✔ [================================================] 100% quay.io/minio/minio:RELEASE.2022-09-17T00-09-45Z minio-2
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Starting containers DONE
✔ Started local/monk-minio/stack

🔩 templates/local/monk-minio/stack
 ├─🧊 Peer minio-1
 │  └─🔩 templates/local/monk-minio/minio1
 │     └─📦 9e0ec943410c5afb117ef2bbdd9eb341-l-monk-minio-minio1-monk-minio
 │        ├─🧩 quay.io/minio/minio:RELEASE.2022-09-17T00-09-45Z
 │        ├─💾 /var/lib/monkd/volumes/monk-minio1/data1 -> /data1
 │        └─💾 /var/lib/monkd/volumes/monk-minio1/data2 -> /data2
 └─🧊 Peer minio-2
    ├─🔩 templates/local/monk-minio/nginx
    │  └─📦 2c6a8b3277368ab240e288271631066f-inio-nginx-nginx-reverse-proxy
    │     ├─🧩 docker.io/bitnami/nginx:latest
    │     ├─🔌 open tcp 13.50.14.172:9000 (0.0.0.0:9000) -> 9000
    │     └─🔌 open tcp 13.50.14.172:9001 (0.0.0.0:9001) -> 9001
    └─🔩 templates/local/monk-minio/minio2
       └─📦 7a57bedd1aeeed1912911529273fc420-l-monk-minio-minio2-monk-minio
          ├─🧩 quay.io/minio/minio:RELEASE.2022-09-17T00-09-45Z
          ├─💾 /var/lib/monkd/volumes/monk-minio2/data2 -> /data2
          └─💾 /var/lib/monkd/volumes/monk-minio2/data1 -> /data1

💡 You can inspect and manage your above stack with these commands:
	monk logs (-f) local/monk-minio/stack - Inspect logs
	monk shell     local/monk-minio/stack - Connect to the container's shell
	monk do        local/monk-minio/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```


## Variables
The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable                     	| Description                               	|
|------------------------------	|-------------------------------------------	|
| monk_minio_port               | Minio Node Port, Default: 9000 	               |
| monk_console_port             | Minio Node Console Port, Default 9001                     	|
| monk_minio_admin_password     | Minio Admin Password, Default: password                     	|
| monk_minio_admin_username     | Minio Admin Username, Default: admin                     	|
| listen_port                   | Minio LB Port Default: 81                     	|
| listen_api_port               | Minio LB Console Port Default: 80                     	|



## Stop, remove and clean up workloads and templates

```bash
monk purge -x -a
```