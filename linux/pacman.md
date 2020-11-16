# pacman 

## List all installed packages by size

```bash
$ expac "%n %m" -l'\n' -Q $(pacman -Qq) | sort -rhk 2 | less
```

## Search packages only by name

```bash
$ pacman -Slq | grep 
```

## Downgrade 

```bash
$ pacman -U /var/cache/pacman/pkg/package-old_version.pkg.tar.type
```
