# Network

Useful networking commands

### Get Gateway IP

```
ip r | grep default | cut -d ' ' -f 3
```

### Get the name of the actively used network interfaces

```bash
route | grep '^default' | grep -o '[^ ]*$'
```

### Get Internal IP Address:

```bash
ifconfig | grep -Eo 'inet (addr:)?([0-9]*\.){3}[0-9]*' | grep -Eo '([0-9]*\.){3}[0-9]*' | grep -v '127.0.0.1'
```

### Get Sent/Received Bytes

```
cat /sys/class/net/eth0/statistics/rx_bytes
cat /sys/class/net/eth0/statistics/rx_packets
cat /sys/class/net/eth0/statistics/tx_packets
cat /sys/class/net/eth0/statistics/tx_bytes
```

### Check If You're Online

```
ping -q -w 1 -c 1 $gateway> /dev/null && echo 1 || echo 0
```
