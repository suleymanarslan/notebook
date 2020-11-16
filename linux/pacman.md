# pacman 

## List all installed packages by size

```bash
$ expac "%n %m" -l'\n' -Q $(pacman -Qq) | sort -rhk 2 | less
```

## Search packages only by name

```bash
$ pacman -Slq | grep 
```

## Downgrade a package

```bash
$ pacman -U /var/cache/pacman/pkg/package-old_version.pkg.tar.type
```

## Downgrade kernel

```bash
$ pacman -U linux-4.15.8-1-x86_64.pkg.tar.xz linux-headers-4.15.8-1-x86_64.pkg.tar.xz 
``
