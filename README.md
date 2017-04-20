[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: http://nzbget.net/
[hub]: https://hub.docker.com/r/lsioarmhf/nzbget/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/nzbget
[![](https://images.microbadger.com/badges/version/lsioarmhf/nzbget.svg)](https://microbadger.com/images/lsioarmhf/nzbget "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/nzbget.svg)](http://microbadger.com/images/lsioarmhf/nzbget "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/nzbget.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/nzbget.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-armhf/lsioarmhf-nzbget)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-armhf/job/lsioarmhf-nzbget/)

[NZBGet](http://nzbget.net/) is a usenet downloader, written in C++ and designed with performance in mind to achieve maximum download speed by using very little system resources.

[![nzbget](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/nzbget-banner.png)][appurl]

## Usage

```
docker create \
	--name nzbget \
	-p 6789:6789 \
	-e PUID=<UID> -e PGID=<GID> \
	-e TZ=<timezone> \
	-v </path/to/appdata>:/config \
	-v <path/to/downloads>:/downloads \
	lsioarmhf/nzbget
```

This container is based on alpine linux with s6 overlay. For shell access whilst the container is running do `docker exec -it nzbget /bin/bash`.

You can choose between ,using tags, various branch versions of nzbget, no tag is required to remain on the main branch.

Add one of the tags,  if required,  to the linuxserver/nzbget line of the run/create command in the following format, linuxserver/nzbget:testing

#### Tags
+ **testing**

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 6789` - NZBGet WebUI Port
* `-v /config` - NZBGet App data
* `-v /downloads` - location of downloads on disk
* `-e PGID` for for GroupID - see below for explanation
* `-e PUID` for for UserID - see below for explanation
* `-e TZ` for timezone EG. Europe/London


### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARMHF VERSION`

Webui can be found at  `<your-ip>:6789` and the default login details (change ASAP) are 

`login:nzbget, password:tegbzn6789`

To allow scheduling, from the webui set the time correction value in settings/logging.

To change umask settings.

![](http://i.imgur.com/A4VMbwE.png)

scroll to bottom, set umask like this (example shown for unraid)

![](http://i.imgur.com/mIqDEJJ.png)

## Info
* Shell access whilst the container is running: `docker exec -it nzbget /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f nzbget`


* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' nzbget`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/nzbget`

## Versions

+ **20.04.17:** Add testing branch.
+ **03.02.17:** Rebase alpine linux 3.5.
+ **14.10.16:** Add version layer information.
+ **30.09.16:** Fix umask.
+ **13.09.16:** Initial Release.
