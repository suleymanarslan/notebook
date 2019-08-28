# Filesystems

## List Information

List information about filesystems (type, usage, etc.)

```bash
$ df -Th
```

Or, using `fdisk`:

```bash
$ fdisk -l
```

## Format

Format as Ext4:

```bash
$ mkfs.ext4 /dev/sdc1
```

Format as exFat:

```bash
$  mkexfatfs /dev/sdc1
```

Format as fat32:

```bash
$ mkdosfs -F 32 -I /dev/sdc1
```

## Change Label

Ext*;

```bash
$ e2label /dev/sdc1 "mydiskname"
```

NTFS:

```bash
$ ntfslabel /dev/sda5 NTFS_DIR
```

Exfat:

```bash
$ exfatlabel /dev/sdb1 newlabel
```

Fat32:

```bash
$ fatlabel /dev/device NewName
```
