# System Recovery Playbook

## Booting to wrong kernel

Due to a failed upgrade or a bad boot entry, wrong kernel version could cause boot failure. In this case, follow these steps;

Check the current kernel: 

```
uname -r
```

Compare it with installed kernel;

```
pacman -Q linux
```

Make sure correct partition and a valid kernel img path is specified in the boot entry. I use Refind, so it'll be at ` /boot/refind_linux.conf`;

```
"Boot with defaults"    "root=UUID=ee5ac81a-e0b6-4e55-961f-52f3bd9e9763  rootfstype=ext4 rw add_efi_memmap initrd=boot\initramfs-linux.img"
```

Using recovery disk, enter into the system and run upgrade again;

```
$ mount /dev/sdaX /mnt
$ chroot /mnt
$ pacman -Syu
```

The upgrade should re-install the Linux (downgrade it if it doesn't) and watch the logs for rebuild of the image (`initramfs-linux.img`) - note the path and point it from the boot entry if necessary.
