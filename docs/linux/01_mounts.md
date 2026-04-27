# Mounts

Mounting is the process of making a filesystem accessible at a certain point in the Linux directory tree. When you mount a device, such as a hard drive, USB stick, or network share, its filesystem becomes available for use under a specified directory, known as the mount point.

## Common Mount Commands

- `mount`: Used to attach filesystems to the directory tree.
- `umount`: Used to detach filesystems.

### Example: Mounting a USB Drive

```bash
sudo mount /dev/sdb1 /mnt/usb
```

This command mounts the device `/dev/sdb1` to the directory `/mnt/usb`.

### Example: Unmounting

```bash
sudo umount /mnt/usb
```

This command unmounts the filesystem from `/mnt/usb`.

## Persistent Mounts

To make mounts persistent across reboots, add an entry to the `/etc/fstab` file:

```txt
/dev/sdb1   /mnt/usb   ext4   defaults   0   2
```

This ensures the device is automatically mounted at boot.

## Viewing Mounted Filesystems

Use the `df` or `mount` command to see currently mounted filesystems:

```bash
df -h
mount
```
