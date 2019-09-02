# External Disks

See also [filesystems.md](./filesystems.md)

## List

Using `fdisk`:

```
$ fdisk -l
```

By UUID:

```bash
ls -l /dev/disk/by-uuid/
```

## Create Mount Point

```bash
$ sudo mkdir /media/usb
$ sudo chown -R pi:pi /media/usb
```

## Manually Mount

```bash
$ sudo mount /dev/sda1 /media/usb -o uid=pi,gid=pi
```

## Unmount

```bash
$ sudo umount /media/usb
```

## Auto-mount

Add following line to the end of `/etc/fstab`:

```fstab
UUID=18A9-9943 /media/usb vfat auto,nofail,noatime,users,rw,uid=pi,gid=pi 0 0
```
