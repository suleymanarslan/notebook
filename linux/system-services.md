# System Services

Index of Contents:

* [systemd](#systemd)
* [upstart](#upstart)

## systemd



### Control Systemd Services

Some useful `systemctl` commands:
* start
* stop
* restart
* reload
* status
* is-enabled
* enable
* disable
* mask
* unmask
* list-units

Restart `systemd` scanning for new or changed units;

```bash
systemctl daemon-reload
```

Toggle a service with one-liner:

```
if [[  "`systemctl is-active NetworkManager`" != "active" ]]; then sudo systemctl start NetworkManager; else sudo systemctl stop NetworkManager; fi

```

See which units are failing;

```bash
systemctl list-units --state=failed
```

See logs of a specific unit;

```bash
sudo journalctl -xu dhcpcd@enp0s3.service --since today
```

Analysize the boot time:

```bash
$ systemd-analyze
```

List the started unit files, sorted by the time each of them took to start up:

```bash
$ systemd-analyze blame
```

See boot units as chain:

```bash
$ systemd-analyze critical-chain
```

### Create New Services

Create a `service` file and save it to `/etc/system.d/system` folder.

```
[Unit]
Description=Monitor battery

[Service]
Type=simple
ExecStart=/bin/bash /home/azer/.happy-desktop/bin/monitor-battery
Environment=DISPLAY=:0
Environment=XAUTHORITY=%h/.Xauthority
Environment=DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
User=azer

[Install]
WantedBy=multi-user.target
```

Then enable & start it:

```bash
$ systemctl enable monitor-battery
$ systemctl start monitor-battery
```

### Timers

To run a service every 10 seconds, create a `.timer` file in same folder with same name;

```
[Timer]
OnUnitInactiveSec=10

[Install]
WantedBy=timers.target
```

Enable & start the timer service:

```bash
$ systemctl enable foobar.service
```

Check the timers: 

```bash
$ sudo systemctl list-timers
```

## upstart

* Logs are saved to /var/log/{app}

#### Commands:

* `initctl list`
* `initctl status myapp`
* `initctl start myapp`

Service can be used, too;

* `sudo service goweb status`
* `sudo service goweb start`

Syntax Check:
* `init-checkconf /etc/init/goweb.conf`

#### Example script:

```
description "A stupid golang http listener"

start on filesystem or runlevel [2345]
stop on runlevel [!2345]

setuid www-data
setgid www-data

env API_KEY=abcdefgh

respawn
respawn limit 5 2

chdir /opt

pre-start script
    # Source File
    . /path/to/env/file
end script

script
    # Start Listener
    /opt/listen
end script
```
