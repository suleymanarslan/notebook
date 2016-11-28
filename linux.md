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
Lists all available fonts in the system. 

```
fc-list | grep Monaco
```

#### nl
Adds line numbers to beginning of each line

#### powertop
Lists processes by their energy consume.

#### yes
Approve all confirmations

```
yes | pacman -S yolo
```

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

## makefiles

#### multiline strings

It's possible as long as the variable is exported

```make
export COMPONENT_HTML
create-component:
  define COMPONENT_HTML
import html from "choo/html"

const view = (state, prev, send) => html`
$(name)
`

export default view
```
  endef

  @echo "$$COMPONENT_HTML" > ui/components/${name}.js

## timezones

#### list all regions:

```bash
find /usr/share/zoneinfo/. -maxdepth 1 -type d | cut -d "/" -f6 | sed '/^$/d'
```

## dialogs

#### opening a menu with bunch of lines

```bash
regionsArray=()

while read i name; do
  regionsArray+=($i "$name")
done <<< "$regions"

selected=$(dialog --stdout \
                  --title "Timezones" \
                  --backtitle "Happy Hacking Linux" \
                  --ok-label "Next" \
                  --no-cancel \
                  --menu "Select a continent or ocean from the menu:" \
                  20 50 30 \
                  "${regionsArray[@]}")
```

## Conditions

#### Check if a variable is empty:

```bash
if [[ -z "${foobar// }" ]]; then
fi
```

#### Check if a variable is not empty:

```bash
[[ -n "${foobar// }" ]]
```

#### Check if a file exists:

```bash
if [ -f $FILE ];
then
   echo "File $FILE exists."
else
   echo "File $FILE does not exist."
fi
```

## loops

#### Iterate Files

```bash
for i in *; do echo $i; done
```

## irssi

* Auto-connect to a network: `/server ADD -auto -network NetworkName irc.host.com 6667`
* Auto-join to channels: `/channel ADD -auto #channel NetworkName password`
* Switch to a window: `M-[number]` use letters when for windows beyond 9: `M-[q|w|e|r|t|y]`
* Close window: `/wc`
* Save config: `/save`
* Load a script: `/script load awm`
* Set theme: `/set theme weed`
