# linux

## Useful Commands

#### chroot
  Opens a new TTY on given root directory.

#### [dialog](#dialogs)
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

#### fc-list
  Lists fonts available in the system.

  ```bash
  fc-list | grep Monaco
  ```

#### nl
  Adds line numbers to beginning of each line

#### powertop
  Lists processes by their energy consume.

#### yes
  Approve all confirmations

#### du
  Checks size of a folder.

  ```bash
  du -sh /
  ```

#### ncdu
  Disk usage analyzer with CLI UI with ncurses.

#### expac
  Data extraction tool for ALPM (Arch Linux Package Management).

  To list packages by their size;
  ```bash
  expac "%n %m" -l'\n' -Q $(pacman -Qq) | sort -rhk 2 | less
  ```

  ```
  yes | pacman -S yolo
  ```

#### ip link show

Lists network interfaces in the system.

#### command_exists

  Definition:
  ```bash
  command_exists () {
      type "$1" &> /dev/null ;
  }
  ```

  Usage:

  ```
  if command_exists foo ; then
      echo "yo"
  fi
  ```

  ```bash
  yes | pacman -S yolo
  ```

#### pkill -f

Kills a process partially matching given pattern;

```
pkill -f pattern
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

#### slugify a string

```bash
sed -e 's/[^[:alnum:]]/-/g' | tr -s '-' | tr A-Z a-z
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

## timezones

#### list all regions:

```bash
find /usr/share/zoneinfo/. -maxdepth 1 -type d | cut -d "/" -f6 | sed '/^$/d'
```

## Managing Services

Use `systemctl` command to control the services. Example;

```bash
systemctl restart slim.service
```

Some useful `systemctl` commands:
* start
* stop
* restart
* reload
* status
* is-enabled
* enable
* disable
* mask
* unmask
* list-units

Restart `systemd` scanning for new or changed units;

```bash
systemctl daemon-reload
```

See which units are failing;

```bash
systemctl list-units --state=failed
```

See logs of a specific unit;

```bash
sudo journalctl -xu dhcpcd@enp0s3.service --since today
```

## Irssi
* Auto-connect to a network: `/server ADD -auto -network NetworkName irc.host.com 6667`
* Auto-join to channels: `/channel ADD -auto #channel NetworkName password`
* Switch to a window: `M-[number]` use letters when for windows beyond 9: `M-[q|w|e|r|t|y]`
* Close window: `/wc`
* Save config: `/save`
* Load a script: `/script load awm`
* Set theme: `/set theme weed`

## Building Custom Arch ISO

#### Step 1: Create Chroot Base System

```bash
$ pacman -S devtools git make --needed
$ mkarchroot /tmp/chroot base
$ git clone git://projects.archlinux.org/archiso.git
$ make -C archiso/archiso DESTDIR=/tmp/chroot install
$ arch-chroot /tmp/chroot
```

#### Step 2: Customize

```
mknod /dev/loop0 b 7 0
echo 'Server = http://ftp.osuosl.org/pub/archlinux/$repo/os/x86_64' >> /etc/pacman.d/mirrorlist
pacman -S devtools libisoburn squashfs-tools
```

And install necessary packages.

#### Step 3: Build The ISO

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

## xmonad

* After making a change hit `xmonad --recompile` to check errors, then `mod+r` to reload the config.

## network

#### Get the name of the actively used network interfaces

```bash
route | grep '^default' | grep -o '[^ ]*$'
```


#### Get Internal IP Address:

```bash
ifconfig | grep -Eo 'inet (addr:)?([0-9]*\.){3}[0-9]*' | grep -Eo '([0-9]*\.){3}[0-9]*' | grep -v '127.0.0.1'
```

#### Get Sent/Received Bytes

```
cat /sys/class/net/eth0/statistics/rx_bytes
cat /sys/class/net/eth0/statistics/rx_packets
cat /sys/class/net/eth0/statistics/tx_packets
cat /sys/class/net/eth0/statistics/tx_bytes
```

#### Check If You're Online

```
ping -q -w 1 -c 1 $gateway> /dev/null && echo 1 || echo 0
```

#### Get Gateway IP

```
ip r | grep default | cut -d ' ' -f 3
```
