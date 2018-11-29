# fstab

## New Disk

Get UUID of the disk that you want to mount:

```bash
$ ls -la /dev/disks/by-uuid
```

Figure out the filesystem type of the disk you want to mount:

```bash
$ lsblk -f
```

If mountpoint is under `/home`, find out user's UID and GID:

```bash
$ id [username]
$ id -g [username]
```

Add a new line to `/etc/fstab` with the values collected:

```
UUID={UUID} /home/username/Shared vfat,user,owner,utf8,rw,umask=022,uid=1000,gid=1000 0 0
```

Apply the changes by reloading fstab:

```bash
$ mount -a
```
