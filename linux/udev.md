# udev

## Monitor Changes

```
$ sudo udevadm monitor
```

## Add a rule

```
$ cat /etc/udev/rules.d/98-monitor-hotplug.rules 
KERNEL=="card0", SUBSYSTEM=="drm", ACTION=="change", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/ben/.Xauthority", RUN+="/bin/bash /path/to/script.sh"  
```

## Reload 

```
$ $ cat /etc/udev/rules.d/98-monitor-hotplug.rules 
KERNEL=="card0", SUBSYSTEM=="drm", ACTION=="change", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/ben/.Xauthority", RUN+="/bin/bash /path/to/script.sh"  
```
