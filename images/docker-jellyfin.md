---
title: jellyfin
---
<!-- DO NOT EDIT THIS FILE MANUALLY  -->
<!-- Please read the https://github.com/linuxserver/docker-jellyfin/blob/master/.github/CONTRIBUTING.md -->

# [linuxserver/jellyfin](https://github.com/linuxserver/docker-jellyfin)

[![Scarf.io pulls](https://scarf.sh/installs-badge/linuxserver-ci/linuxserver%2Fjellyfin?color=94398d&label-color=555555&logo-color=ffffff&style=for-the-badge&package-type=docker)](https://scarf.sh/gateway/linuxserver-ci/docker/linuxserver%2Fjellyfin)
[![GitHub Stars](https://img.shields.io/github/stars/linuxserver/docker-jellyfin.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=github)](https://github.com/linuxserver/docker-jellyfin)
[![GitHub Release](https://img.shields.io/github/release/linuxserver/docker-jellyfin.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=github)](https://github.com/linuxserver/docker-jellyfin/releases)
[![GitHub Package Repository](https://img.shields.io/static/v1.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=linuxserver.io&message=GitHub%20Package&logo=github)](https://github.com/linuxserver/docker-jellyfin/packages)
[![GitLab Container Registry](https://img.shields.io/static/v1.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=linuxserver.io&message=GitLab%20Registry&logo=gitlab)](https://gitlab.com/linuxserver.io/docker-jellyfin/container_registry)
[![Quay.io](https://img.shields.io/static/v1.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=linuxserver.io&message=Quay.io)](https://quay.io/repository/linuxserver.io/jellyfin)
[![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/jellyfin.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=pulls&logo=docker)](https://hub.docker.com/r/linuxserver/jellyfin)
[![Docker Stars](https://img.shields.io/docker/stars/linuxserver/jellyfin.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=stars&logo=docker)](https://hub.docker.com/r/linuxserver/jellyfin)
[![Jenkins Build](https://img.shields.io/jenkins/build?labelColor=555555&logoColor=ffffff&style=for-the-badge&jobUrl=https%3A%2F%2Fci.linuxserver.io%2Fjob%2FDocker-Pipeline-Builders%2Fjob%2Fdocker-jellyfin%2Fjob%2Fmaster%2F&logo=jenkins)](https://ci.linuxserver.io/job/Docker-Pipeline-Builders/job/docker-jellyfin/job/master/)
[![LSIO CI](https://img.shields.io/badge/dynamic/yaml?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=CI&query=CI&url=https%3A%2F%2Fci-tests.linuxserver.io%2Flinuxserver%2Fjellyfin%2Flatest%2Fci-status.yml)](https://ci-tests.linuxserver.io/linuxserver/jellyfin/latest/index.html)

[Jellyfin](https://github.com/jellyfin/jellyfin) is a Free Software Media System that puts you in control of managing and streaming your media. It is an alternative to the proprietary Emby and Plex, to provide media from a dedicated server to end-user devices via multiple apps. Jellyfin is descended from Emby's 3.5.2 release and ported to the .NET Core framework to enable full cross-platform support. There are no strings attached, no premium licenses or features, and no hidden agendas: just a team who want to build something better and work together to achieve it.

## Supported Architectures

We utilise the docker manifest for multi-platform awareness. More information is available from docker [here](https://github.com/docker/distribution/blob/master/docs/spec/manifest-v2-2.md#manifest-list) and our announcement [here](https://blog.linuxserver.io/2019/02/21/the-lsio-pipeline-project/).

Simply pulling `lscr.io/linuxserver/jellyfin:latest` should retrieve the correct image for your arch, but you can also pull specific arch images via tags.

The architectures supported by this image are:

| Architecture | Available | Tag |
| :----: | :----: | ---- |
| x86-64 | ✅ | amd64-\<version tag\> |
| arm64 | ✅ | arm64v8-\<version tag\> |
| armhf | ❌ | |

## Version Tags

This image provides various versions that are available via tags. Please read the descriptions carefully and exercise caution when using unstable or development tags.

| Tag | Available | Description |
| :----: | :----: |--- |
| latest | ✅ | Stable Jellyfin releases |
| nightly | ✅ | Nightly Jellyfin releases |
## Application Setup

Webui can be found at `http://<your-ip>:8096`

More information can be found on the official documentation [here](https://jellyfin.org/docs/general/quick-start.html).

## Hardware Acceleration

### Intel

Hardware acceleration users for Intel Quicksync will need to mount their /dev/dri video device inside of the container by passing the following command when running or creating the container:

`--device=/dev/dri:/dev/dri`

We will automatically ensure the abc user inside of the container has the proper permissions to access this device.

To enable the OpenCL based DV, HDR10 and HLG tone-mapping, please refer to the OpenCL-Intel mod from here:

https://mods.linuxserver.io/?mod=jellyfin

### Nvidia

Hardware acceleration users for Nvidia will need to install the container runtime provided by Nvidia on their host, instructions can be found here:

https://github.com/NVIDIA/nvidia-docker

We automatically add the necessary environment variable that will utilise all the features available on a GPU on the host. Once nvidia-docker is installed on your host you will need to re/create the docker container with the nvidia container runtime `--runtime=nvidia` and add an environment variable `-e NVIDIA_VISIBLE_DEVICES=all` (can also be set to a specific gpu's UUID, this can be discovered by running `nvidia-smi --query-gpu=gpu_name,gpu_uuid --format=csv` ). NVIDIA automatically mounts the GPU and drivers from your host into the jellyfin docker container.

### OpenMAX (Raspberry Pi)

Hardware acceleration users for Raspberry Pi MMAL/OpenMAX will need to mount their `/dev/vcsm` and `/dev/vchiq` video devices inside of the container and their system OpenMax libs by passing the following options when running or creating the container:

```
--device=/dev/vcsm:/dev/vcsm
--device=/dev/vchiq:/dev/vchiq
-v /opt/vc/lib:/opt/vc/lib
```

### V4L2 (Raspberry Pi)

Hardware acceleration users for Raspberry Pi V4L2 will need to mount their `/dev/video1X` devices inside of the container by passing the following options when running or creating the container:

```
--device=/dev/video10:/dev/video10
--device=/dev/video11:/dev/video11
--device=/dev/video12:/dev/video12
```

## Usage

To help you get started creating a container from this image you can either use docker-compose or the docker cli.

### docker-compose (recommended, [click here for more info](https://docs.linuxserver.io/general/docker-compose))

```yaml
---
version: "2.1"
services:
  jellyfin:
    image: lscr.io/linuxserver/jellyfin:latest
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - JELLYFIN_PublishedServerUrl=192.168.0.5 #optional
    volumes:
      - /path/to/library:/config
      - /path/to/tvseries:/data/tvshows
      - /path/to/movies:/data/movies
    ports:
      - 8096:8096
      - 8920:8920 #optional
      - 7359:7359/udp #optional
      - 1900:1900/udp #optional
    restart: unless-stopped
```

### docker cli ([click here for more info](https://docs.docker.com/engine/reference/commandline/cli/))

```bash
docker run -d \
  --name=jellyfin \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -e JELLYFIN_PublishedServerUrl=192.168.0.5 `#optional` \
  -p 8096:8096 \
  -p 8920:8920 `#optional` \
  -p 7359:7359/udp `#optional` \
  -p 1900:1900/udp `#optional` \
  -v /path/to/library:/config \
  -v /path/to/tvseries:/data/tvshows \
  -v /path/to/movies:/data/movies \
  --restart unless-stopped \
  lscr.io/linuxserver/jellyfin:latest

```

## Parameters

Docker images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

### Ports (`-p`)

| Parameter | Function |
| :----: | --- |
| `8096` | Http webUI. |
| `8920` | Optional - Https webUI (you need to set up your own certificate). |
| `7359/udp` | Optional - Allows clients to discover Jellyfin on the local network. |
| `1900/udp` | Optional - Service discovery used by DNLA and clients. |

### Environment Variables (`-e`)

| Env | Function |
| :----: | --- |
| `PUID=1000` | for UserID - see below for explanation |
| `PGID=1000` | for GroupID - see below for explanation |
| `TZ=Etc/UTC` | specify a timezone to use, see this [list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List). |
| `JELLYFIN_PublishedServerUrl=192.168.0.5` | Set the autodiscovery response domain or IP address. |

### Volume Mappings (`-v`)

| Volume | Function |
| :----: | --- |
| `/config` | Jellyfin data storage location. *This can grow very large, 50gb+ is likely for a large collection.* |
| `/data/tvshows` | Media goes here. Add as many as needed e.g. `/data/movies`, `/data/tv`, etc. |
| `/data/movies` | Media goes here. Add as many as needed e.g. `/data/movies`, `/data/tv`, etc. |

#### Miscellaneous Options

| Parameter | Function |
| :-----:   | --- |

## Environment variables from files (Docker secrets)

You can set any environment variable from a file by using a special prepend `FILE__`.

As an example:

```bash
-e FILE__PASSWORD=/run/secrets/mysecretpassword
```

Will set the environment variable `PASSWORD` based on the contents of the `/run/secrets/mysecretpassword` file.

## Umask for running applications

For all of our images we provide the ability to override the default umask settings for services started within the containers using the optional `-e UMASK=022` setting.
Keep in mind umask is not chmod it subtracts from permissions based on it's value it does not add. Please read up [here](https://en.wikipedia.org/wiki/Umask) before asking for support.

## Optional Parameters

The [official documentation for ports](https://jellyfin.org/docs/general/networking/index.html) has additional ports that can provide auto discovery.

Service Discovery (`1900/udp`) - Since client auto-discover would break if this option were configurable, you cannot change this in the settings at this time. DLNA also uses this port and is required to be in the local subnet.

Client Discovery (`7359/udp`) - Allows clients to discover Jellyfin on the local network. A broadcast message to this port with "Who is Jellyfin Server?" will get a JSON response that includes the server address, ID, and name.

```
  -p 7359:7359/udp \
  -p 1900:1900/udp \
```

The [official documentation for environmentals](https://jellyfin.org/docs/general/administration/configuration.html) has additional environmentals that can provide additional configurability such as migrating to the native Jellyfin image.

## User / Group Identifiers

When using volumes (`-v` flags), permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user `PUID` and group `PGID`.

Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.

In this instance `PUID=1000` and `PGID=1000`, to find yours use `id user` as below:

```bash
  $ id username
    uid=1000(dockeruser) gid=1000(dockergroup) groups=1000(dockergroup)
```

## Docker Mods

[![Docker Mods](https://img.shields.io/badge/dynamic/yaml?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=jellyfin&query=%24.mods%5B%27jellyfin%27%5D.mod_count&url=https%3A%2F%2Fraw.githubusercontent.com%2Flinuxserver%2Fdocker-mods%2Fmaster%2Fmod-list.yml)](https://mods.linuxserver.io/?mod=jellyfin "view available mods for this container.") [![Docker Universal Mods](https://img.shields.io/badge/dynamic/yaml?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=universal&query=%24.mods%5B%27universal%27%5D.mod_count&url=https%3A%2F%2Fraw.githubusercontent.com%2Flinuxserver%2Fdocker-mods%2Fmaster%2Fmod-list.yml)](https://mods.linuxserver.io/?mod=universal "view available universal mods.")

We publish various [Docker Mods](https://github.com/linuxserver/docker-mods) to enable additional functionality within the containers. The list of Mods available for this image (if any) as well as universal mods that can be applied to any one of our images can be accessed via the dynamic badges above.

## Support Info

* Shell access whilst the container is running:
  * `docker exec -it jellyfin /bin/bash`
* To monitor the logs of the container in realtime:
  * `docker logs -f jellyfin`
* Container version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' jellyfin`
* Image version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' lscr.io/linuxserver/jellyfin:latest`

## Versions

* **12.09.23:** - Take ownership of plugin directories.
* **04.07.23:** - Deprecate armhf. As announced [here](https://www.linuxserver.io/blog/a-farewell-to-arm-hf)
* **07.12.22:** - Rebase master to Jammy, migrate to s6v3.
* **11.06.22:** - Switch to upstream repo's ffmpeg5 build.
* **05.01.22:** - Specify Intel iHD driver versions to avoid mismatched libva errors.
* **25.12.21:** - Fix video device group perms error message.
* **10.12.21:** - Rework readme, disable template sync.
* **22.09.21:** - Pull only the server, web and ffmpeg packages instead of the wrapper.
* **23.06.21:** - Add log message if device permissions are incorrect. Pin jellyfin dependency versions to prevent upstream apt repo issues. Deprecate the `bionic` tag.
* **21.05.21:** - Add nvidia.icd file to fix missing tonemapping using Nvidia HW.
* **20.01.21:** - Add Jellyfin Binary Environmentals
* **20.01.21:** - Deprecate `UMASK_SET` in favor of UMASK in baseimage, see above for more information.
* **23.11.20:** - Rebase to Focal, branch off Bionic.
* **22.07.20:** - Ingest releases from Jellyfin repo.
* **28.04.20:** - Replace MMAL/OMX dependency device `/dev/vc-mem` with `/dev/vcsm` as the former was not sufficient for raspbian.
* **11.04.20:** - Enable hw decode (mmal) on Raspberry Pi, update readme instructions, add donation info, create missing default transcodes folder.
* **11.03.20:** - Add Pi V4L2 support, remove optional transcode mapping (location is selected in the gui, defaults to path under `/config`).
* **30.01.20:** - Add nightly tag.
* **09.01.20:** - Add Pi OpenMax support.
* **02.10.19:** - Improve permission fixing for render & dvb devices.
* **31.07.19:** - Add AMD drivers for vaapi support on x86.
* **13.06.19:** - Add Intel drivers for vaapi support on x86.
* **07.06.19:** - Initial release.
