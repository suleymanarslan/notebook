# Useful Linux Commands

Index of Contents:

* [awk](#awk)
* [chroot](#chroot)
* [convert](#convert)
* [date](#date)
* [dialog](#dialog)
* [du](#du)
* [expac](#expac)
* [fc-list](#fc-list)
* [ffmpeg](#ffmpeg)
* [file](#file)
* [grep](#grep)
* [htop](#htop)
* [hwclock](#hwclock)
* [iotop](#iotop)
* [ip](#ip)
* [ncdu](#ncdu)
* [nethogs](#nethogs)
* [nl](#nl)
* [pidof](#pidof)
* [pkill](#pkill)
* [powertop](#powertop)
* [sed](#sed)
* [setxkbmap](#setxkbmap)
* [tee](#tee)
* [timedatectl](#timedatectl)
* [tree](#tree)
* [xargs](#xargs)
* [xev](#xev)
* [xdpyinfo](#xdipyinfo) 
* [yes](#yes)


## awk

Select particular columns and print out;

```bash
lsblk | awk '{print $1,$4}'
# sda 8GB
```

## convert

Resize an image by keeping the proportions, changing the format:

```bash
convert -scale "$resolution^" ~/wallpaper.jpg  /tmp/wallpaper.png
```

Add a black transparent layer on top and some text in the center;

```bash
convert ~/wallpaper.jpg \
            -scale "$resolution^" \
            -fill black -colorize 50% \
            -font System-San-Francisco-Display \
            -fill "#ffffff33" \
            -gravity center -pointsize 30 -annotate +0-200 'A man sees in the world what he carries in his heart. — Goethe' \
            $lockpng
```

Rotate the image:

```bash
convert  image.png -rotate -90 image-copy.png
```

## chroot

Opens a new TTY on given root directory.

## date

Get unix timestamp:

```
date +%s
```

Get date & time nicely formatted;

```
date '+%d %h %H:%M'
# 22 Jun 01:42
```

## dialog
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

## du
Checks size of a folder.

  ```bash
  du -sh /
  ```

## expac
Data extraction tool for ALPM (Arch Linux Package Management).

To list packages by their size;
```bash
  expac "%n %m" -l'\n' -Q $(pacman -Qq) | sort -rhk 2 | less
```

```
  yes | pacman -S yolo
```

## fc-list
Lists fonts available in the system.

```bash
fc-list | grep Monaco
```

## file

Returns file info. It's especially useful on images;

```bash
file logo.png
# PNG image data, 16 x 16, 8-bit/color RGBA, non-interlaced
```

## ffmpeg

Record screen:

```bash
$ sleep 10; ffmpeg -y -video_size 1366x680 -framerate 25 -f x11grab -i :0.0+0,80 output.mp4
## sleep {X}:                      prepare for X seconds before start recording
## -y:                             overwrite output.mp4 if exists
## -video_size {width}x{height}:   make frame size to width x height
## -framerate:                     frame per second
## -f x11grab:                     the encoder used, you shouldn't modify this =/
## -i {a}.{b}+{left},{top}:        record screen {a}.{b}(FYI: X server $DISPLAY) with offset from left top corner of screen to {left} {top}
```

Trim video by time:

```bash
$ ffmpeg -y -i output.mp4 -ss 3 -t 11 myclip.mp4; ffplay myclip.mp4
## -i:         specify which input file
## --ss {n}:   trim {n} seconds from begining
## -t {d}:     secify the duration of myclip.mp4
## ffplay:     play myclip.mp4 once the encoding ends
```

Output series of PNG files;
```bash
$ rm -rf frames
$ mkdir frames
$ ffmpeg -i myclip.mp4 -vf scale=320:-1:flags=lanczos,fps=10 frames/ffout%03d.png
## frames/:            make a new directory to store output pictures
## scale={width}:-1:   make pictures at scale of {width} with calculated height
## flags={whatever}:   some MAGIC
## fps={x}:            make pictures with playback at {x}fps
## ffout%03d.png:      file name with 001, 002, ..., 999
```

Put all PNG files together in a GIF:

```bash
$ convert -delay 3 -loop 0 -dither None -colors 80 "frames/ffout*.png" -fuzz "10%" -layers OptimizeFrame "output.gif"
## -delay {f}: skip {f} frames between each frame in GIF, making GIF playing fast
## -loop 0: make GIF loop forever
## -color {c}: Make about {c} colors in available in GIF
## -fuzz "10%": fuzz each frame, would make GIF not recognizable
## -layers: some MAGIC
```

## grep

Match patterns with text, print not matched;

```bash
grep -oFf patterns.txt text.txt | grep -vFf - patterns.txt
```

## htop

Interactive process viewer. Useful keybindings:

* `/` Search
* `\` Filter
* `,` Choose the sorting criteria
* `k` Send kill signal to selected process
* `u` Filter results by user
* `t` Open/close tree mode
* `-` or `+` Collapse/uncollapse process trees
* `H` Turn off displaying threads

## hwclock

Show hardware clock:

```
hwclock --show
```

Set hardware clock from system clock;

```
hwclock --systohc
```

## iotop

Sorts processes by disk writes, and show how much and how frequently programs are writing to the disk.

## ip

List network interfaces in the system:

```bash
ip link show
```

Manage routing tables:

```
ip r
```
## ncdu
Disk usage analyzer with CLI UI with ncurses.

## nethogs

htop for network. lists processes by their network traffic.

## nl
Adds line numbers to beginning of each line.

```bash
cat foobar.txt | nl
```

## pidof

Find process id of a running program:

```
pidof nginx
```

It might return multiple pids (e.g nginx have worker processes). Specify `-s` parameter to get only one pid:

```
pidof -s nginx
```

## pkill

Kill a process partially matching given pattern;

```
pkill -f pattern
```

## powertop
Lists processes by their energy consume.

## sed

Display nth line in a large file:

```bash
sed '26577519q;d'
```

Replace nth line in a large file:

```bash
sed -i '26577519s/ &#3;/ /' content.rdf.u8
```

Uncomment matching line:

```bash
sed -i -e '/^#en_US/s/^#//' /etc/locale.
```

Slugify a string:

```bash
sed -e 's/[^[:alnum:]]/-/g' | tr -s '-' | tr A-Z a-z
```

## setxkbmap

Sets the keyboard layout:

```
setxkbmap tr -variant alt -option lv3:ralt
```

## tee

It's used for splitting the output of a program so we can both display it and also save it.

For example, add a new entry to hosts file;

```
echo "127.0.0.1 foobar" | sudo tee -a /etc/hosts
```

## timedatectl

Check the system time and timezone info:

```
timedatectl
```

Set system clock:

```
timedatectl set-time "yyyy-MM-dd hh:mm:ss"
```

Set timezone:

```
timedatectl set-timezone America/Los_Angeles
```

## tree

Lists contents of a directory in tree-like format.

```
tree
```

Show hidden files:

```
tree -a
```

Show only directories:

```
tree -d
```

## xargs

Build an execute commands from standard input

```bash
xargs -n 1 curl < download.txt
```

## xdpyinfo

Get screen resolution:

```bash
xdpyinfo | awk '/dimensions/{print $2}'
```

## xev

Creates a window and lets you see the keyboard events. Useful when you modify keybindings.

## xprop

Gives information about window properties. 

## yes
Approve all confirmations

```bash
  yes | pacman -S yolo
```
