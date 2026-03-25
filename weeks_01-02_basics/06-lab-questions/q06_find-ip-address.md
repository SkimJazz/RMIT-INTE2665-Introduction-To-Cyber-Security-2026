# 6. Find the IP address and computer name of your machine.

Below commands will show the IP address.


```bash
ifconfig
```
> `ifconfig` has been deprecated on some systems in favor of `ip a`.
> `ip a` output looks heaps better and more detailed.

```bash
hostname
```

Whats the question trying to get at?

The question is asking you to identify the two different network identities of your machine by finding its **IP address(Network identity)** and **hostname (Logical identity)**. 

The IP address is used for network communication, while the hostname is a human-readable identifier for the machine. Together, they define how the machine is recognized on a network.

So basically:
- IP address = Network identity
- Hostname = Logical identity


```zsh
┌──(kali㉿kali)-[~]
└─$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet xx.x.x.xx  netmask xxx.xxx.xxx.x  broadcast xx.x.x.xxx


lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet xxx.x.x.x  netmask xxx.x.x.x
```
Key parts:
- `eth0` = Network interface name (may vary) -> wired/virtual network adapter
- `wlan0` = Wireless network interface (if applicable)
- `lo` = Loopback interface (always present)

Only interfaces that are UP and RUNNING have active IP addresses. And interfaces marked `UP` and with an `inet` value are the ones currently connected to a network (most relevant for this question).
- `inet xx.x.x.xx` = IPv4 address
- `inet xxx.x.x.x` = Loopback address (localhost)

**Why this matters in security terms**

Knowing how to identify your own system is foundational for:

- Network scanning (nmap)
- Firewall rules
- Log correlation
- Incident response (“which host was affected?”)

An IP address can:

- Change (DHCP)
- Be spoofed
- Identify network location

A hostname:

- Helps humans track systems
- Appears in alerts and logs


**Discussion:**

_The computer name of the system can be found using the hostname command, which displays the system’s hostname. The IP address can be identified using the ifconfig command, which shows network interfaces and their assigned IP addresses. The IP address represents the system’s network identity, while the hostname represents its logical name._
