# Display

## Find out the DPI

```
xdpyinfo | grep -B 2 resolution
```

## Set DPI Manually

```
xrandr --dpi 220
```

And update `.Xresources`:

```
Xft.dpi:                    220
```
