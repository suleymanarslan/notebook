# Swap

## Mount Swap Partition

Create a Swap partition using partitioning tools like `cfdisk` or `parted`. Then format the partition as swap;

```
$ mkswap /dev/sdXY
```

Enable it;

```bash
$ swapon /dev/sdXY
```

Get UUID of the partition:

```bash
$ sudo blkid /dev/sdXY
```

And add following line into `/etc/fstab`

```fstab
UUID=? none   swap    sw      0       0
```

List swap devices and their sizes:

```bash
$ swapon -s
```

See which swap devices are being used:

```bash
$ cat /proc/swaps
```

See total, used and free swap space:

```
$ cat /proc/meminfo | grep Swap
```

Or:

```
$ cat /proc/swaps
```

## Swapiness

The swappiness sysctl parameter represents the kernel's preference (or avoidance) of swap space. Swappiness can have a value between 0 and 100, the default value is 60. A low value causes the kernel to avoid swapping, a higher value causes the kernel to try to use swap space. Using a low value on sufficient memory is known to improve responsiveness on many systems.
To check the current swappiness value:

```bash
$ cat /proc/sys/vm/swappiness
```

To temporarily set the swappiness value:

```bash
$ sysctl vm.swappiness=10
```

To set the swappiness value permanently, edit a `sysctl` configuration file:

```bash
echo "vm.swappiness=10" > /etc/sysctl.d/99-sysctl.conf
```
