# Useful Linux Commands

Index of Contents:

* [awk](#awk)
* [chroot](#chroot)
* [column](#column)
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
* [mount](#mount)
* [pidof](#pidof)
* [pkill](#pkill)
* [powertop](#powertop)
* [sed](#sed)
* [setxkbmap](#setxkbmap)
* [sort](#sort)
* [uniq](#uniq)
* [tee](#tee)
* [timedatectl](#timedatectl)
* [tree](#tree)
* [xargs](#xargs)
* [ufw](#ufw)
* [xev](#xev)
* [xdpyinfo](#xdipyinfo)
* [xdotool](#xdotool)
* [xprop](#xprop)
* [yes](#yes)



## awk

Select particular columns and print out;

```bash
lsblk | awk '{print $1,$4}'
# sda 8GB
```


Filter out the values in the column if they're lower than 3000;

```bash
awk '$0 > 3000  {print ;}'
```

Calculate sum of the numbers in the selected column:

```bash
awk '{SUM+=$0}END{print SUM}' data.txt
```

Calculate avg of the numbers in the selected column;

```bash
awk '{ sum += $1 } END { if (NR > 0) print sum / NR }'
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

## column

Equalize column width of given file.

```
$ cat > text.txt
id name age                                                                                                               
1 azer 30
2 fuji 1
3 nova 27
```


```
$ column -t col.txt                                                                                                    
id  name  age                                                                                                             
1   azer  30
2   fuji  1
3   nova  27
```

Change delimiter to `:`:

```
column -t -s ':'
```

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

Lists font families available in the system:

```bash
fc-list : family
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
$ ffmpeg -y -i output.mp4 -ss 3 -t 11 myclip.mp4
## -i:         specify which input file
## --ss {n}:   trim {n} seconds from begining
## -t {d}:     secify the duration of myclip.mp4
## ffplay:     play myclip.mp4 once the encoding ends
```

Get video resolution:

```bash
$ ffprobe -v error -select_streams v:0 -show_entries stream=width,height -of csv=s=x:p=0 merged.mp4
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

Trim an mp3 file:

```
ffmpeg -i file.mp3 -ss 00:00:20 -to 00:00:40 -c copy file-2.mp3
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

## mount

A bind mount is an alternate view of a directory tree. Classically, mounting creates a view of a storage device as a directory tree. A bind mount instead takes an existing directory tree and replicates it under a different point. The directories and files in the bind mount are the same as the original. Any modification on one side is immediately reflected on the other side, since the two views show the same data.

Under Linux, bind mounts are available as a kernel feature. You can create one with the mount command, by passing either the --bind command line option or the bind mount option. The following two commands are equivalent:

`
mount --bind /some/where /else/where
`

[source](https://unix.stackexchange.com/questions/198590/what-is-a-bind-mount)

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

Get value of a field from JSON file:

```bash
sed -n 's/\s*\"foo":\s*"\(.*\)\"/\1/p' config.json
```

## setxkbmap

Sets the keyboard layout:

```
setxkbmap tr -variant alt -option lv3:ralt
```

## sort

Sort the contents of a file alphabetically, in reverse order, by number, by month. It can also remove duplicates.

```
$ cat > file.txt
abhishek
chitransh
satish
rajan
naveen
divyam
harsh
```

```
$ sort file.txt
abhishek
chitransh
divyam
harsh
naveen 
rajan
satish
```

## uniq

Filters duplicate lines.

```
$ cat > file.txt
foo
bar
foo
qux
```

```
$ cat file.txt | uniq -c
2 foo
1 bar
1 qux
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

## xdotool

Get mouse location.

```
xdotool getmouselocation --shell
```

## xev

Creates a window and lets you see the keyboard events. Useful when you modify keybindings.

## xprop

Gives information about window properties. 

## ufw

Allow access to specified from anywhere:

```bash
ufw allow 22
```

Allow only trusted ip to specified port;

```bash
ufw allow from TRUSTED_IP to any port 9200
```

Enable it

```bash
ufw enable
```

Check the status

```bash
ufw status
```

## yes
Approve all confirmations

```bash
  yes | pacman -S yolo
```
