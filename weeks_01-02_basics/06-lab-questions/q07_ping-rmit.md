# 7. Test Network Connectivity

Check if your machine can reach RMIT: Using the `ping` command:

```bash
ping rmit.edu.au
```

Okay. So what is happening here?

The `ping` command sends **ICMP Echo Request packets** to the specified hostname (rmit.edu.au) and waits for ICMP Echo Reply packets in response. This tests whether the target host is reachable over the network and measures the round-trip time for messages sent from the source to the destination.

So. This is not just about "can you type `ping rmit.edu.au` and see if it works".

The `ping` command will test whether:

1. DNS resolution is working (hostname → IP)
2. Network connectivity exists between your machine and the target host
3. The target host is online and responding to ICMP requests -> Is ICMP traffic allowed?
4. Your system can reach an external host -> test the networks internet access

> ALL FOUR of these need to be true for `ping` to succeed.

The following is suposed to be example output when using the `ping` command:

Let's ping google.com as an example:

```zsh
┌──(kali㉿kali)-[~]
└─$ ping google.com
PING google.com (142.250.66.238) 56(84) bytes of data.
64 bytes from syd15s15-in-f14.1e100.net (142.250.66.238): icmp_seq=1 ttl=255 time=49.9 ms
64 bytes from syd15s15-in-f14.1e100.net (142.250.66.238): icmp_seq=2 ttl=255 time=48.7 ms
...
```

Now let's ping rmit.edu.au:

```zsh
┌──(kali㉿kali)-[~]
└─$ ping rmit.edu.au
PING rmit.edu.au (131.170.0.105) 56(84) bytes of data.
^C
--- rmit.edu.au ping statistics ---
6 packets transmitted, 0 received, 100% packet loss, time 5099ms
```

RMIT appears to **block ICMP echo replies (traffic)**, resulting in 100% packet loss. GOOGLE DOSES NOT.

What is happening here?

Your system:

- Successfully resolves the hostname → DNS works
- Successfully sends ICMP Echo Requests
- Receives no Echo Replies

The following line proves it. I `ctrl+c` after 5 seconds coz I know RMIT would block shit.

```zsh
6 packets transmitted, 0 received, 100% packet loss, time 5099ms
```

So:
❌ Not a DNS problem
❌ Not a routing problem
❌ Not a Kali problem
✅ A firewall / security policy decision

Why is RMIT blocking ICMP (this is textbook security)

Universities, enterprises, and governments often:

- Block ICMP echo replies
- Still allow:
  HTTP (80),
  HTTPS (443), and
  DNS (53)

Why?

**Security reasons:**

- Prevent network reconnaissance
- Reduce attack surface
- Hide internal network behaviour
- Mitigate ICMP-based scanning & DoS

Google chooses to allow ICMP because:

- They use it for global diagnostics
- They operate at internet scale
- They accept the trade-off

Google is basically a Glory hole at a truck stop bathroom.

**SUMMARY / KEY POINTS:**

- ping will keep sending requests
- It prints(output) only when replies are received
- No replies = no per-packet output
- Talking ≠ ping replies.

If there were no communication:

- DNS would fail
- Or routing would fail

**DISCUSSION**

_The ping command was used to test connectivity to rmit.edu.au. Although no ICMP echo replies were received, the hostname successfully resolved to an IP address and ICMP packets were transmitted. This indicates that the system can reach the host, but ICMP echo replies are likely blocked by the remote server’s firewall._
