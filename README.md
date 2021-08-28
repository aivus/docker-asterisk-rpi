# Asterisk RPi + chan_dongle

[![Build and push](https://github.com/aivus/docker-asterisk-rpi/actions/workflows/build_and_push.yml/badge.svg)](https://github.com/aivus/docker-asterisk-rpi/actions/workflows/build_and_push.yml)

This repository contains docker configuration and provides images for [Asterisk](https://www.asterisk.org/) with [chan_dongle](https://github.com/wdoekes/asterisk-chan-dongle).

Docker repository: [aivus/asterisk-rpi](https://hub.docker.com/r/aivus/asterisk-rpi)

GitHub repository: [aivus/docker-asterisk-rpi](https://github.com/aivus/docker-asterisk-rpi/)

# Basic usage

## Using images from hub.docker.com

Dockerhub contains docker images with compiled binaries for all available ARM platforms of Raspberry Pi: armv6, armv7, arm64.

To start container run command like:
```sh
docker run -d --name asterisk --volume ~/asterisk:/etc/asterisk --network host --device /dev/ttyUSB0:/dev/ttyUSB0 --device /dev/ttyUSB1:/dev/ttyUSB1 --device /dev/ttyUSB2:/dev/ttyUSB2 --restart always aivus/asterisk-rpi:master
```

where:
* `~/asterisk` is a directory with asterisk configuration. (**Don't have configuration? See [How to create sample configuration](#how-to-create-sample-configuration)**)
* `--device /dev/ttyUSBX:/dev/ttyUSBX` is a path to the USB devices of Huawei UMTS card

## Build yourself

To build the image locally run:

```sh
docker build -t asterisk https://raw.githubusercontent.com/aivus/docker-asterisk-rpi/master/Dockerfile
```


# How to create sample configuration
To start the Asterisk you need to have a configuration skeleton.
Fortunately, this default configuration could be copied right from the image.

Follow next steps to copy sample configuration from the image to host machine. Directory called `asterisk` will be created in the current working directory.

```sh
docker create --name asterisk-samples aivus/asterisk-rpi:master
docker cp asterisk-samples:/opt/asterisk-samples/ asterisk
docker rm asterisk-samples
```
