# Laptop Issues

## Wake Up After Suspend

Source: [Arch Linux Wiki](https://wiki.archlinux.org/index.php/Mac#Wake_Up_After_Suspend)

Occasionally the Macboook Air may wake up immediately after suspend. To fix this:

```bash
cat /proc/acpi/wakeup
```

Check to see that XHC1 and LID0 are enabled. If they are, disabling them will fix the problem. After disabling them, the only way to wake up your computer from suspend is by using the power button.

To do this type to following command (vim can be any cli editor)

```bash
$ sudo vim /etc/systemd/system/suspend-fix.service
```

Then add the following text and save:

```systemctl
[Unit]
Description=Fix for the suspend issue

[Service]
Type=oneshot
ExecStart=/bin/sh -c "echo XHC1 > /proc/acpi/wakeup && echo LID0 > /proc/acpi/wakeup"

[Install]
WantedBy=multi-user.target
```

And then run the following:

```bash
$ systemctl enable suspend-fix.service
$ systemctl start suspend-fix.service
```

Disabling only XHC1 is not recommended if you have this bug, since it may result in glitchy behavior.
