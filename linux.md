# linux

## Useful Commands

#### chroot
Opens a new TTY on given root directory.

#### dialog
You can create UI dialogs with it on command-line easily. For example;

```bash
usernameDialog () {
    username=$(dialog --stdout \
                      --title "Creating Users" \
                      --backtitle "Happy Hacking Linux" \
                      --ok-label "Done" \
                      --nocancel \
                      --inputbox "Choose your username" 8 50)
}
```

#### nl
Adds line numbers to beginning of each line

#### powertop
Lists processes by their energy consume.

#### yes

Essential for scripting commands that asks user verification.

```bash
yes | pacman -S yolo
```

## partitioning

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

## creating users

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

## arch linux installation

* [Create Partitions](#partitioning)
* Make sure boot (/mnt/boot) & root (/mnt) mounted.
* Run `pacstrap` to install the base: `pacstrap /mnt`
* Update FS Tab: `genfstab -U /mnt >> /mnt/etc/fstab`
* Switch to the new root: `arch-chroot /mnt`
* Install GRUB
* Localize:
  * Select timezone with `tzselect`
  * Generate /etc/adjtime: `hwclock --systohc`
  * Uncomment en_US lines in /etc/locale.gen: `sed -i -e '/^#en_US/s/^#//' /etc/locale.gen`
  * Generate locales with `locale-gen`
  * `echo "LANG=en_US.UTF-8" >> /etc/locale.conf`
  * `echo "FONT=Lat2-Terminus16" >> /etc/vconsole.conf`
* [Create users](#create-users)
* Done

## sed

#### Uncomment matching line with sed

```bash
sed -i -e '/^#en_US/s/^#//' /etc/locale.
```

## awk

#### Select columns

```bash
lsblk | awk '{print $1,$4}'
# sda 8GB
```

## iterating input by line and columns

```bash
while read col1 col2 ; do
  echo "$col1 $col2"
done < input.txt
```
