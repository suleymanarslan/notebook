# Trash

Commands:

```
trash-put           trash files and directories.
trash-empty         empty the trashcan(s).
trash-list          list trashed files.
trash-restore       restore a trashed file.
trash-rm            remove individual files from the trashcan.
```

Remove files older than X days:

```bash
trash-empty <days>
```

Bind <delete> button in Ranger:

```bash
map <DELETE> shell -s trash-put %s
```
