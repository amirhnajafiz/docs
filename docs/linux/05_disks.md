# Disks

To see only physical disks (no partitions), run:

```sh
lsblk -d
```

If you want to see more details, run:

```sh
sudo lshw -class disk
```

Before using a disk, create a new file system.

```sh
sudo mkfs.ext4 /dev/sdX#
```

The mount it.

```sh
sudo mkdir -p /mnt/device
sudo mount /dev/sdX# /mnt/device
```

## Capacity check

A quick command to check free space on disks is:

```sh
df -h
# Filesystem      Size  Used Avail Use% Mounted on
# /dev/sda2       200G  198G  2G   100% /
```

By running `du` we can dig deeper into space usage:

```sh
sudo du -xhd1 / | sort -hr | head -20
# 45G /var
# 32G /home
# 12G /usr
```

* du stands for disk usage
* the x flag tells to stay on same filesystem only
* the h flag tells to export as human readable
* the d1 flag tells one level deep

> An alternative solution is `ncdu`, which scans the disk usage.

## Hidden files

Often `du` output doesn't match with `df` output. In that case, you may be facing with hidden files.

One good command to check hidden files is `lsof` (list open files). This can help you track open files in memory.

> Also if you have docker on a machine, you can use `docker system df`. Docker often takes too much disk space.

Also you might have unmounted loop devices somewhere in the root disk. You can see them using:

```sh
sudo losetup -a
sudo losetup /dev/loop1 /mnt/loop1
```

## Ultimate solution

Both `du` and `ncdu` take too much time (overhead and permissions issues). Because, we you start scanning from root, you have too many virtual filesystems like /proc or /sys. You also might have separate partiotions, like having /home on NFS. The partitions are actully causing this overhead and permissions issues.

A good solution is to use bind mount to mount your root filesystem into a new mount point. By using bind, the system will automatically ignore separate partitions. This results in having the actull files in your root disk mirrored in a new mount point.

```sh
sudo mkdir /mnt/os
sudo mount -o bind / /mnt/os
sudo du -sh /mnt/os/* | sort -h
```

This would return a response in few seconds.
