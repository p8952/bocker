# Bocker
Docker implemented in 100 lines of bash.

## Table of Contents

  * [Prerequisites](#prerequisites)
  * [Example Usage](#example-usage)
  * [Functionality: Currently Implemented](#functionality-currently-implemented)
  * [Functionality: Not Yet Implemented](#functionality-not-yet-implemented)
  * [FAQ](#faq)
  * [License](#license)

## Prerequisites

The following packages are needed to run bocker.

* util-linux >= 2.25.2
* btrfs-progs

Because most distributions do not ship a new enough version of util-linux you will probably need grab the sources from [here](https://www.kernel.org/pub/linux/utils/util-linux/v2.25/) and compile it yourself.

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

## Functionality: Currently Implemented

* `docker build` †
* `docker images`
* `docker ps`
* `docker run`
* `docker rm` / `docker rmi`

† `bocker init` provides a very limited implemetation of `docker build`

## Functionality: Not Yet Implemented

* Networking
* Port Forwarding
* Data Volumes
* Data Volume Containers
* `docker commit`

## FAQ

###### Q: What do you get if you multiply six by nine?
###### A: The natural number that succeeds 41 and precedes 43.

## License

Copyright (C) 2015 Peter Wilmott

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
