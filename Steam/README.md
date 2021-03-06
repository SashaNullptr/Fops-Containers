# Steam

Steam with OpenGL support and GPU pass through.

## Prerequisites

This container makes use of the [Nvidia container runtime](https://github.com/NVIDIA/nvidia-container-runtime)
in order to pass through host system GPU to the container. As such the host system will
need a compatible Nvidia GPU installed.

## Host Set-up | Ubuntu Linux

Share the X server

```shell
xhost +
```

Note sharing the X server like is _not secure in the slightest_ and will be
addressed in future iterations of this container.

Install proprietary Nvidia drivers


```shell
sudo ubuntu-drivers autoinstall
```

Install Nvidia container runtime

```shell
sudo apt install nvidia-container-runtime
```

## Run the Docker Image

We need to set some things up so container's X server is shared with the host.
Notably we need to share the host's DISPLAY and `/dev/dri`

In order to prevent Stream from having to do an initial update every time the container
starts we want map a host volume to `/home/steam/.steam/`.

In order to get persistent game storage we need to map a volume to `/opt/steam/.local/share/Steam`.

A docker run command that sets everything up properly is shown below.

```shell
docker run \
  -it \
  --runtime=nvidia \
  --device=/dev/dri \
  --user steam
  --volume /tmp/.X11-unix:/tmp/.X11-unix:rw \
  --volume ./steam_games:/home/steam/.steam/ \
  --volume ./steam_data:/opt/steam/.local/share/Steam \
  --env DISPLAY=$DISPLAY
  sashanullptr/steam:latest
```

## Use in Docker-Compose

Integrating this container into a `docker-compose` might look like:

```yaml
steam:
  restart: on-failure
  image: 'sashanullptr/steam:latest'
  runtime: nvidia
  environment:
    - DISPLAY=$DISPLAY
  user: steam
  volumes:
    - '/tmp/.X11-unix:/tmp/.X11-unix:rw'
    - ./steam_games:/home/steam/.steam/
    - ./steam_data:/opt/steam/.local/share/Steam
  devices:
    - /dev/dri
  healthcheck:
      test: steamcmd +login anonymous +quit || exit 1
      interval: 10s
      timeout: 2s
      retries: 5
```
