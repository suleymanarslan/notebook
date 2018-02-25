# Tips

## Irssi
* Auto-connect to a network: `/server ADD -auto -network NetworkName irc.host.com 6667`
* Auto-join to channels: `/channel ADD -auto #channel NetworkName password`
* Switch to a window: `M-[number]` use letters when for windows beyond 9: `M-[q|w|e|r|t|y]`
* Close window: `/wc`
* Save config: `/save`
* Load a script: `/script load awm`
* Set theme: `/set theme weed`

## Xmonad

* After making a change hit `xmonad --recompile` to check errors, then `mod+r` to reload the config.

## Increase /tmp Size

Unmount /tmp first:

```
umount -l /tmp
```

And mount it to another folder:

```
mount --bind /path/to/folder/tmp /tmp
```
