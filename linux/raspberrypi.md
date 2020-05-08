# Raspberry PI

#### General Configuration

Run `raspi-config`

#### Vertical Screen

Add to `/boot/config.txt`:

```
display_rotate=0 Normal
display_rotate=1 90 degrees
display_rotate=2 180 degrees
NOTE: You can rotate both the image and touch interface 180º by entering lcd_rotate=2 instead
display_rotate=3 270 degrees
display_rotate=0x10000 horizontal flip
display_rotate=0x20000 vertical flip
```
