# boGate

A small Yocto-based project for getting familiar with building firmware for Raspberry Pi 4.

## Hardware

* [Raspberry-pi 4](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) #NOTE boGate is tested on raspberry pi 4 model b with 2GB RAM.

## Prerequisites

* Install [Podman](https://podman.io/docs/installation)

## Get started

The image is built and uploaded as a GitHub Actions artifact when workflow dispatch is triggered. Publishing builds from tags will be added later.

Clone the repo and cd into it:

```bash
git clone git@github.com:Dexter9532/boGate.git && cd boGate
```

Set up a virtual environment and install `kas`:

```bash
python3 -m venv .venv
```

```bash
. .venv/bin/activate
```

```bash
pip install kas
```

Manually build image:

```bash
kas-container build
```

## Flash image

Locate the SD card device:

```bash
lsblk
```

Unmount any mounted partitions on the SD card:

```bash
sudo umount /dev/sdb1 /dev/sdb2
```

Replace `/dev/sdb` with your SD card device and flash the image:

```bash
bzcat build/tmp/deploy/images/raspberrypi4-64/core-image-minimal-raspberrypi4-64.rootfs-<timestamp>.wic.bz2 | sudo dd of=/dev/sdb bs=4M status=progress conv=fsync
```

Flush pending writes before removing the card:

```bash
sync
```
