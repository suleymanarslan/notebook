# Bluetooth

Open up `bluetoothctl` to scan and pair with bluetooth devices.

```
$ bluetoothctl
```

List devices:

```
devices
```

To run single command, pass `--`:

```
$ bluetoothctl -- info # lists connected devices
```

## Commands

### power

Turns on and off bluetooth.

```
power on
```

### agent

Filters out device types. To scan only keyboards:

```
agent KeyboardOnly
```

To make it default agent:

```
default-agent
```

### pairable

Switch to pairable mode:

```
pairable on
```

### scan

Scan bluetooth devices nearby:

```
scan on
```

will output:

```
Discovery started
[CHG] Controller 06:05:04:03:02:01 Discovering: yes
```

### pair

Copy the bluetooth address from `scan` output and run:

```
pair 01:02:03:04:05:06
```

### connect

Establish connection between two devices:

```
connect 01:02:03:04:05:06
```

Run `trust` if necessary.
