# Kernel Modules

List currently loaded kernel modules:

```bash
$ lsmod
```

Show info about a kernel module:

```bash
$ modinfo foobar
```

Unload a kernel module:

```bash
$ modrobe -r foobar # or rmmod foobar
```

Load a kernel module:

```bash
$ modprobe foobar
```

To load a module in the boot;

```
$ echo "foobar" > /etc/modules-load.d/foobar.conf
```

## Blacklisting

Example: `/etc/modprobe.d/nobeep.conf`

```
blacklist pcspkr
```

To verify if a module is blacklisted;

```
journalctl -b | grep foobar
```
