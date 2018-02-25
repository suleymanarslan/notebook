# Arch Linux

Index of Contents

* [Build AUR Package](#build-aur-package)
* [Installation](#installation)
* [Custom ISO](#custom-iso)

## Build AUR Package

* Obtain `PKGBUILD`
* Run `makepkg -Acs`
* Install from the tarball running `sudo pacman -U x.pkg.tar.xz`

## Installation

Download ISO and create a bootable USB stick;

In Linux:
```bash
dd bs=4M if=/path/to/archlinux.iso of=/dev/sdx status=progress && sync
```

In OSX:

```bash
sudo dd if=path/to/arch.iso of=/dev/rdiskX bs=1m
```

After booting the USB, follow these steps;

* [Create Partitions](#partitioning)
* Make sure boot (/mnt/boot) & root (/mnt) mounted.
* Run `pacstrap` to install the base: `pacstrap /mnt`
* Update FS Tab: `genfstab -U /mnt >> /mnt/etc/fstab`
* Switch to the new root: `arch-chroot /mnt`
* Install GRUB
* Localize:
  * [Select timezone](#timezones)
  * Generate /etc/adjtime: `hwclock --systohc`
  * Uncomment en_US lines in /etc/locale.gen: `sed -i -e '/^#en_US/s/^#//' /etc/locale.gen`
  * Generate locales with `locale-gen`
  * `echo "LANG=en_US.UTF-8" >> /etc/locale.conf`
  * `echo "FONT=Lat2-Terminus16" >> /etc/vconsole.conf`
* [Create users](#creating-users)
* Done

### Partitioning

  * Command-line tools: parted, fdisk, cfdisk (with UI)
  * List disks and partitions by `fdisk -l` or `lsblk`
  * The simple and popular layout is boot & root;

  ```bash
  parted /dev/sda --script mklabel msdos \
      mkpart primary ext4 1MiB 512MiB \
      set 1 boot on \
      mkpart primary ext4 512MiB 100%
  ```

  * Don't forget formatting them as ext4: `yes | mkfs.ext4 /dev/sda1`

### Creating Users

  This bash function I wrote for happy-hacker-linux installer shows the steps of creating a user.

```bash
createUser () {
    useradd -m -s /usr/bin/zsh $1
    echo "$1:$2" | chpasswd

    echo "$1 ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
    echo $1 > /etc/hostname
    echo "127.0.1.1	$1.localdomain	$1" >> /etc/hosts
}
```

### Timezones

View your time info:

```bash
timedatectl
```

List all regions:

```bash
find /usr/share/zoneinfo/. -maxdepth 1 -type d | cut -d "/" -f6 | sed '/^$/d'
```

Or, select your timezone interactively:

```bash
tzselect
```

Then set your timezone:

```bash
timedatectl set-timezone Asia/Makassar
```

### date

Print current date formatted:

```
date '+%d %h %H:%M'
```

Set current date:

```
date --set="23 June 1988 10:00:00"
```

Or time:

```
date --set="10:00:00"
```

## Custom ISO

### Step 1: Create Chroot Base System

```bash
$ pacman -S devtools git make --needed
$ mkarchroot /tmp/chroot base
$ git clone git://projects.archlinux.org/archiso.git
$ make -C archiso/archiso DESTDIR=/tmp/chroot install
$ arch-chroot /tmp/chroot
```

### Step 2: Customize

```
mknod /dev/loop0 b 7 0
echo 'Server = http://ftp.osuosl.org/pub/archlinux/$repo/os/x86_64' >> /etc/pacman.d/mirrorlist
pacman -S devtools libisoburn squashfs-tools
```

And install necessary packages.

### Step 3: Build The ISO

```
cp -r /usr/share/archiso/configs/baseline /tmp
cd /tmp/baseline
./build.sh
exit
```

Now, you will be out of your chroot, with the built ISO at the file path of:

```
/tmp/chroot/tmp/baseline/out/<iso>
```
