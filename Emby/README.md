# Emby

[Emby](https://emby.media/index.html) with Hardware accelerated transoding via GPU pass through.

## Prerequisites

This container makes use of the [Nvidia container runtime](https://github.com/NVIDIA/nvidia-container-runtime)
in order to pass through host system GPU to the container. As such the host system will
need a compatible Nvidia GPU installed.

## Host Set-up | Ubuntu Linux

Install proprietary Nvidia drivers


```shell
sudo ubuntu-drivers autoinstall
```

Install Nvidia container runtime

```shell
sudo apt install nvidia-container-runtime
```
