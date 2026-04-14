# boGate

A small Yocto-based project for getting familiar with building firmware for Raspberry Pi 4.

## Get started

The image is built and uploaded as a GitHub Actions artifact when workflow dispatch is triggered. Publishing builds from tags will be added later.

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
kas-container build meta-bogate/kas/firmware.yml
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
