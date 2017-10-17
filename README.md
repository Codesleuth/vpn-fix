# vpn-fix

Updates this fix to work on Linux. I will clean this up to _instead_ be multi-platform later.

## Setup (Linux)

Clone this repo

```bash
$ git clone https://github.com/Codesleuth/vpn-fix
```

### Whitelist

Copy `whitelist.sample.txt` to `whitelist.txt` and add in IP addresses and/or hosts you want to access through the VPN **One per each line**.

e.g.

```
nearform.com
github.com
1.2.3.4
5.6.7.8
```

### Connect to your VPN

Connect and check your VPN has assumed the device ID of `ppp0`

```bash
$ route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.1.254   0.0.0.0         UG    596    0        0 enx18dbf25d268e
1.1.1.1         0.0.0.0         255.255.255.255 UH    0      0        0 ppp0
169.254.0.0     0.0.0.0         255.255.0.0     U     1000   0        0 docker0
172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 docker0
172.18.0.0      0.0.0.0         255.255.0.0     U     0      0        0 br-c20ed15495cd
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 enx18dbf25d268e
```

### Run

Run the `vpn-fix` script, which prints out the hosts it resolves.

```bash
$ sudo ./vpn-fix

Found 1.2.3.4 for host nearform.com
Found 5.6.7.8 for host github.com
```

You can also easily update your whitelist and and run again. The entries will be removed when you disconnect from the VPN so ensure you reconnect if you want to wipe out the list (or use `route del <ip>`).
