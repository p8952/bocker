# Bocker
Docker implemented in 100 lines of bash.

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

Additionally your system will need to be configured with the following.

* A btrfs filesystem mounted under `/var/bocker`
* A network bridge called `bridge0` and an IP of 10.0.0.1/24
* IP forwarding enabled in `/proc/sys/net/ipv4/ip_forward`
* A firewall routing traffic from `bridge0` to a physical interface.

For ease of use a Vagrantfile is included which will build the needed environment.

Even if you meet the above prerequisites you probably still want to **run bocker in a virtual machine**. Bocker runs as root and among other things needs to make changes to your network interfaces, routing table, and firewall rules. **I can make no guarantees that it wont trash your system**.

## Example Usage

```
$ bocker init base-image/
img_74432

$ bocker images
IMAGE_ID
img_74432

$ bocker run img_74432 uname -sro
Linux 3.10.0-123.20.1.el7.x86_64 GNU/Linux

$ bocker ps
CONTAINER_ID       COMMAND
ps_43529           uname -sro

$ bocker rm ps_43529
ps_43529

$ bocker rm img_74432
img_74432
```

## Functionality: Currently Implemented

* `docker build` †
* `docker images`
* `docker ps`
* `docker run`
* `docker rm` / `docker rmi`
* Networking

† `bocker init` provides a very limited implemetation of `docker build`

## Functionality: Not Yet Implemented

* DNS
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
