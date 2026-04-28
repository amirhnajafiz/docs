# DM Delay

Assume that you're device is `/dev/sdX`.

First, get the size in sectors.

```sh
$ blockdev --getsz /dev/sdX
# 4069
```

Create a delayed device (1s on both read and write).

```sh
# <start> <end> delay <dev> <offset> <read_delay_ms> <write_dev> <write_offset> <write_delay_ms>
echo "0 4096 delay /dev/sdX 0 1000 /dev/sdX 0 1000" | dmsetup create delayed_loop
```

Get your mapped device from `/dev/mapper/delayed_loop`.

```sh
sudo mount /dev/mapper/delayed_loop /mnt/delayed_loop
```

Here are some other useful commands:

```sh
# get a list of current dm delay devices
ls /dev/mapper/
# remove a device
sudo dmsetup remove delayed_loop
# see all devices
sudo dmsetup table
# get information of a device
sudo dmsetup info delayed_loop
# suspend a device
sudo dmsetup suspend delayed_loop
# resume a device
sudo dmsetup resume delayed_loop
# change an existng device
echo "0 4096 delay /dev/sdX 0 2000" | sudo dmsetup reload delayed_loop
sudo dmsetup resume delayed_loop
# drop OS paged cache if delay is not happening
echo 3 | sudo tee /proc/sys/vm/drop_caches
```
