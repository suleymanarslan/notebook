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

## Blacklisting

Example: `/etc/modprobe.d/nobeep.conf`

```
blacklist pcspkr
```
