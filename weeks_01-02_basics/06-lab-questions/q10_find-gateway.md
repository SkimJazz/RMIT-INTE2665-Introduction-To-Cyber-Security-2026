# 10. Find Default Gateway & Routing Table

## Question:

"Find the default gateway and IP Address of your local network. (Hint: `netstat -r`)"

```zsh
netstat -r
```

## Bro! What's that mean?

It’s testing whether you understand routing, not just commands.

Specifically:

- How your system decides where traffic goes
- Which device is the exit point from your local network
- How to identify your network range

## Commands used:

```zsh
netstat -r
```

## Example Usage | Output:

#### Step 1: Run the command

```zsh
netstat -r  # `ip route` is an alternative command for newer systems
```

```zzsh
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
default         cloudmesh       0.0.0.0         UG        0 0          0 eth0
xxx.xxx.xx.x    0.0.0.0         xxx.xxx.xxx.x   U         0 0          0 eth0
```

#### Step 2: Identify the default gateway from the output

```zsh
Destination = default = xxx.xxx.xx.x
```

#### Step 3: Identify your local network

```zsh
Local Network = xxx.xxx.xxx.x/xx
```

## Explanation:

This means:

- Network range: xxx.xxx.xx.x → xxx.xxx.xx.xxx
- Your machine’s IP lives inside this range

## Why this matters in Security:

**Understanding the default gateway is critical for:**

- Traffic interception
- Firewall placement
- Network segmentation
- Man-in-the-middle attacks
- Incident response (“where did the traffic go?”)

**Attackers target gateways.
Defenders monitor them.**

## Summary | Key Points:

- The default gateway is the exit point from your local network.
- The routing table shows how traffic is directed.
- Knowing your network range helps identify devices on the same subnet.

## Discussion:

_The `netstat -r` command displays the system’s routing table. The default gateway is identified by the entry where the destination is listed as default. This gateway is used to route traffic outside the local network. The local network address and subnet mask indicate the network range to which the system belongs._
