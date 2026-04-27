# NFS

NFS (Network File System) allows you to share directories and files with others over a network. It enables users to mount remote directories on their local machines and interact with them as if they were local files.

## Installing NFS

On most Linux distributions, you can install NFS utilities with:

```bash
sudo apt install nfs-common        # Debian/Ubuntu
sudo yum install nfs-utils         # CentOS/RHEL
```

## Mounting an NFS Share

To mount an NFS share, use the `mount` command:

```bash
sudo mount server:/remote/path /mnt/nfs
```

- `server` is the hostname or IP address of the NFS server.
- `/remote/path` is the exported directory on the server.
- `/mnt/nfs` is the local mount point.

## Unmounting an NFS Share

```bash
sudo umount /mnt/nfs
```

## Persistent NFS Mounts

To mount an NFS share automatically at boot, add an entry to `/etc/fstab`:

```txt
server:/remote/path   /mnt/nfs   nfs   defaults   0   0
```

## Viewing NFS Mounts

To see active NFS mounts:

```bash
mount -t nfs
```

Or use `df` to see usage:

```bash
df -hT | grep nfs
```

## Exporting Directories (Server Side)

On the NFS server, edit `/etc/exports` to specify which directories to share:

```txt
/srv/nfs    192.168.1.0/24(rw,sync,no_subtree_check)
```

Then restart the NFS server:

```bash
sudo exportfs -ra
sudo systemctl restart nfs-server
```
