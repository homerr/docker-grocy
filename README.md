[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)](https://linuxserver.io)

The [LinuxServer.io](https://linuxserver.io) team brings you another container release featuring :-

 * regular and timely application updates
 * easy user mappings (PGID, PUID)
 * custom base image with s6 overlay
 * weekly base OS updates with common layers across the entire LinuxServer.io ecosystem to minimise space usage, down time and bandwidth
 * regular security updates

Find us at:
* [Discord](https://discord.gg/YWrKVTn) - realtime support / chat with the community and the team.
* [IRC](https://irc.linuxserver.io) - on freenode at `#linuxserver.io`. Our primary support channel is Discord.
* [Blog](https://blog.linuxserver.io) - all the things you can do with our containers including How-To guides, opinions and much more!
* [Podcast](https://anchor.fm/linuxserverio) - on hiatus. Coming back soon (late 2018).

# PSA: Changes are happening

From August 2018 onwards, Linuxserver are in the midst of switching to a new CI platform which will enable us to build and release multiple architectures under a single repo. To this end, existing images for `arm64` and `armhf` builds are being deprecated. They are replaced by a manifest file in each container which automatically pulls the correct image for your architecture. You'll also be able to pull based on a specific architecture tag.

TLDR: Multi-arch support is changing from multiple repos to one repo per container image.

# [linuxserver/grocy](https://github.com/linuxserver/docker-grocy)
[![](https://img.shields.io/discord/354974912613449730.svg?logo=discord&label=LSIO%20Discord&style=flat-square)](https://discord.gg/YWrKVTn)
[![](https://images.microbadger.com/badges/version/linuxserver/grocy.svg)](https://microbadger.com/images/linuxserver/grocy "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/linuxserver/grocy.svg)](https://microbadger.com/images/linuxserver/grocy "Get your own version badge on microbadger.com")
![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/grocy.svg)
![Docker Stars](https://img.shields.io/docker/stars/linuxserver/grocy.svg)

[Grocy](https://github.com/grocy/grocy) is an ERP system for your kitchen! Cut down on food waste, and manage your chores with this brilliant utulity.

Keep track of your purchaes, how much food you are wasting, what chores need doing and what batteries need charging with this proudly Open Source tool

For more information on grocy visit their website and check it out: https://grocy.info


[![grocy](https://grocy.info/img/grocy_logo.svg)](https://github.com/grocy/grocy)

## Supported Architectures

Our images support multiple architectures such as `x86-64`, `arm64` and `armhf`. We utilise the docker manifest for multi-platform awareness. More information is available from docker [here](https://github.com/docker/distribution/blob/master/docs/spec/manifest-v2-2.md#manifest-list). 

The architectures supported by this image are:

| Architecture | Tag |
| :----: | --- |
| x86-64 | amd64-latest |
| arm64 | arm64v8-latest |
| armhf | arm32v6-latest |

## Usage

Here are some example snippets to help you get started creating a container.

### docker

```
docker create \
  --name=grocy \
  -e PUID=1001 \
  -e PGID=1001 \
  -e TZ=<your timezone, eg Europe/London> \
  -p 9283:80 \
  -v <path to data>:/config \
  --restart unless-stopped \
  linuxserver/grocy
```


### docker-compose

Compatible with docker-compose v2 schemas.

```
---
version: "2"
services:
  grocy:
    image: linuxserver/grocy
    container_name: grocy
    environment:
      - PUID=1001
      - PGID=1001
      - TZ=<your timezone, eg Europe/London>
    volumes:
      - <path to data>:/config
    ports:
      - 9283:80
    mem_limit: 4096m
    restart: unless-stopped
```

## Parameters

Container images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| :----: | --- |
| `-p 80` | will map the container's port 80 to port 9283 on the host |
| `-e PUID=1001` | for UserID - see below for explanation |
| `-e PGID=1001` | for GroupID - see below for explanation |
| `-e TZ=<your timezone, eg Europe/London>` | for specifying your timezone |
| `-v /config` | this will store any uploaded data on the docker host |

## User / Group Identifiers

When using volumes (`-v` flags) permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user `PUID` and group `PGID`.

Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.

In this instance `PUID=1001` and `PGID=1001`, to find yours use `id user` as below:

```
  $ id username
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

&nbsp;
## Application Setup

Grocy is simple to get running. Configure the container with the above instructions, start it, and you can then access it
by visiting http://your.ip:9283 - once the page loads, you can log in with the default username and password of admin / admin



## Support Info

* Shell access whilst the container is running: `docker exec -it grocy /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f grocy`
* container version number 
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' grocy`
* image version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/grocy`

## Versions

* **27.12.18:** - Initial Release.
