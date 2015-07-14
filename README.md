# Bocker
Docker implemented in 100 lines of bash.

## Prerequisites

The following packages are needed to run bocker.

* util-linux 2.25.2
* btrfs-progs 3.16.2


Because RHEL/CentOS 7 does not ship a new enough version of util-linux you will need grab the sources from [here](https://www.kernel.org/pub/linux/utils/util-linux/v2.25/) and compile yourself.

Additionally `/var/bocker` needs to be on a btrfs filesystem.

For ease of use a Vagrantfile is included which will build the needed environment.

## Example Usage

```
$ ./bocker init base-image/
img_e6b698c1-513d-4a40-807c-23b0fe54353a

$ ./bocker images
IMAGE_ID
img_e6b698c1-513d-4a40-807c-23b0fe54353a

$ ./bocker run img_e6b698c1-513d-4a40-807c-23b0fe54353a uname -sro
Linux 3.10.0-123.20.1.el7.x86_64 GNU/Linux

$ ./bocker ps
CONTAINER_ID					            COMMAND
ps_349bf646-06cf-4d98-bcf8-744f59e7e6bb		uname -sro

$ ./bocker rm ps_349bf646-06cf-4d98-bcf8-744f59e7e6bb
ps_349bf646-06cf-4d98-bcf8-744f59e7e6bb

$ ./bocker rm img_e6b698c1-513d-4a40-807c-23b0fe54353a
img_e6b698c1-513d-4a40-807c-23b0fe54353a
```

## Currently Implemented

* `docker build` †
* `docker images`
* `docker ps`
* `docker run`
* `docker rm` / `docker rmi`

† `bocker init` provides a very limited implemetation of `docker build`

## Not Yet Implemented

* Networking
* Port Forwarding
* Data Volumes
* Data Volume Containers
* `docker commit`
