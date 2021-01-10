# Use iPhone as Webcam

Sources: 
* [Using Obs Studio as Virtual Webcam](https://blog.jbrains.ca/permalink/using-obs-studio-as-a-virtual-cam-on-linux)

iPhone:
* Install Obs Camera on the iPhone

Linux:

* Install `usbmuxd` and `obs-plugin-ios-camera-source`
```bash
$ sudo pacman -S usbmuxd
$ systemctl enable usbmuxd.service
$ systemctl start usbmuxd.service
$ yay -S obs-plugin-ios-camera-source-git
```

* Pair iPhone plugged via USB

```
$ idevicepair pair
```

* After pairing, IOSCamera should be available as a source.

Virtual Camera:

* Install `v4l2loopback-dkms`
* Open `obs` and hit `start virtual camera`
* Or, on CLI; `obs --startvirtualcam`
