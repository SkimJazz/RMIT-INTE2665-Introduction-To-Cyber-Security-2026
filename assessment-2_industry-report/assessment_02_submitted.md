# INTE2665 Introduction to Cyber Security – Assessment 2

- School of Computing Technologies
- College of Science, Technology, Engineering and Maths
- RMIT University
- Australia
- March 2026 

## Table of Contents
- [INTE2665 Introduction to Cyber Security – Assessment 2](#inte2665-introduction-to-cyber-security--assessment-2)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Part A: Report](#part-a-report)
    - [**2. Firewall Configuration and Experimental Results (Tasks A–F)**](#2-firewall-configuration-and-experimental-results-tasks-af)
      - [**2.0 Pre-Test Setup and Baseline Validation**](#20-pre-test-setup-and-baseline-validation)
      - [**2.1 Task A - Reject connection on loopback interface**](#21-task-a---reject-connection-on-loopback-interface)
      - [**2.2 Task B - Reject connection at port 22 for SSH**](#22-task-b---reject-connection-at-port-22-for-ssh)
      - [**2.3 Task C - Deny ping and then demonstrate that you can restore ping command functionality**](#23-task-c---deny-ping-and-then-demonstrate-that-you-can-restore-ping-command-functionality)
      - [**2.4 Task D - Reject all traffic coming to port 80**](#24-task-d---reject-all-traffic-coming-to-port-80)
      - [**2.5 Task E - Block incoming traffic connection to the IP address of your virtual machine**](#25-task-e---block-incoming-traffic-connection-to-the-ip-address-of-your-virtual-machine)
      - [**2.6 Task F - Allow traffic coming to port 80 (inbound) but reject accessing IP address 8.8.8.8.**](#26-task-f---allow-traffic-coming-to-port-80-inbound-but-reject-accessing-ip-address-8888)
    - [**3. Testing Method and Validation Process**](#3-testing-method-and-validation-process)
      - [**3.1 Baseline Establishment**](#31-baseline-establishment)
      - [**3.2 Controlled Rule Deployment**](#32-controlled-rule-deployment)
      - [**3.3 Practical Validation Testing**](#33-practical-validation-testing)
      - [**3.4 Verification Using Packet Counters**](#34-verification-using-packet-counters)
      - [**3.5 Restoration and Recovery Validation**](#35-restoration-and-recovery-validation)
    - [**4. Efficient Management of iptables Rulesets**](#4-efficient-management-of-iptables-rulesets)
      - [**4.1 Rule Ordering and Separation of Concerns**](#41-rule-ordering-and-separation-of-concerns)
      - [**4.2 Backup, Rollback, and Change Control**](#42-backup-rollback-and-change-control)
      - [**4.3 Scripted Deployment (Repeatability)**](#43-scripted-deployment-repeatability)
      - [**4.4 Rule Documentation and Comments**](#44-rule-documentation-and-comments)
      - [**4.5 Version Control and Configuration-as-Code**](#45-version-control-and-configuration-as-code)
      - [**4.6 Risk of Misconfiguration**](#46-risk-of-misconfiguration)
    - [**5. Attacks on Packet Filtering Firewalls and Countermeasure Effectiveness**](#5-attacks-on-packet-filtering-firewalls-and-countermeasure-effectiveness)
      - [**5.1 IP Spoofing and Source Routing**](#51-ip-spoofing-and-source-routing)
      - [**5.2 Fragmentation-Based Evasion**](#52-fragmentation-based-evasion)
      - [**5.3 Port Scanning and Stateless Evasion Techniques**](#53-port-scanning-and-stateless-evasion-techniques)
  - [Part B: Reflection](#part-b-reflection)
  - [Conclusion](#conclusion)
  - [References](#references)



## Introduction

This report documents the configuration, testing, and evaluation of a packet filtering firewall
using iptables on a Kali Linux virtual machine. The objective was to implement and validate a series
of firewall behaviours that control traffic by interface, protocol, port, destination address, and
direction (inbound vs outbound). Practical testing was performed from a Windows host machine to
confirm real network behaviour and to ensure that results reflected applied firewall policy rather
than service availability or connectivity issues.

Firewalls are commonly used at organisational boundaries to restrict unwanted inbound traffic and to
limit unauthorised outbound connections. As a technical control, they reduce the exposed attack
surface by permitting only necessary services and denying all other traffic. However, packet
filtering firewalls primarily inspect packet header information and therefore have known
limitations, particularly when threats exploit allowed ports, target higher application layers, or
originate from inside the network.

To address these limitations, cyber security applies a defence-in-depth approach, where technical
controls such as firewalls are combined with monitoring, endpoint protection, authentication, and
administrative controls. This report therefore focuses on both (1) the practical implementation and
verification of iptables rules, and (2) reflection on how firewalls contribute to layered security
in real environments.

## Part A: Report

### **2. Firewall Configuration and Experimental Results (Tasks A–F)**

#### **2.0 Pre-Test Setup and Baseline Validation**

Before applying firewall rules in Tasks A–F, a baseline was established to ensure that any later
connectivity failures were caused by iptables rules (Not by inactive services or network
misconfiguration). The virtual machine was configured in bridged mode so that practical tests could
be executed from the host system (Windows 11) to the VM (Kali Linux) over the local network.

**2.0.1 Baseline firewall state and rollback point**

The default iptables policies were confirmed to be permissive (ACCEPT). A baseline ruleset snapshot
was then saved to support controlled rollback after each experiment (Ref: 2.1.3 Restore
Functionality for snippet).

```bash
sudo iptables -S
sudo iptables-save > open-baseline.rules
```

**2.0.2 Baseline service availability and listening ports**

Core services required for testing were started (SSH, HTTP/Apache, and MariaDB(MySQL)), and their
listening ports were verified on the VM (22/80/3306). This confirmed that the services were
available prior to firewall filtering. Figure 1 shows all required services were active and
listening prior to firewall rule testing. For the purposes of this report, the MySQL/MariaDB service
(3306) was not tested from the host.

```bash
┌──(kali㉿kali)-[~]
└─$ sudo systemctl status ssh apache2 mariadb --no-pager
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: disabled)
     Active: active (running) since Fri 2026-02-13 03:07:02 EST; 19h ago
 Invocation: e2a7c269966b430d92eff50775993bf2
       Docs: man:sshd(8)
             man:sshd_config(5)

● apache2.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/apache2.service; disabled; preset: disabled)
     Active: active (running) since Fri 2026-02-13 03:27:19 EST; 19h ago
 Invocation: 56c2f7fb57ec408e85d20f3958fad81f


● mariadb.service - MariaDB 11.8.3 database server
     Loaded: loaded (/usr/lib/systemd/system/mariadb.service; disabled; preset: disabled)
     Active: active (running) since Fri 2026-02-13 22:53:13 EST; 14s ago
 Invocation: fdbe77cea9b342bbb5dd99bfc747d5e4
       Docs: man:mariadbd(8)
             https://mariadb.com/kb/en/library/systemd/
            .
            .
            .
   Main PID: 43022 (mariadbd)
     Status: "Taking your SQL requests now..."


┌──(kali㉿kali)-[~]
└─$ sudo ss -lntp | grep -E ':22|:80|:3306'
LISTEN 0      80         127.0.0.1:3306      0.0.0.0:*    users:(("mariadbd",pid=43022 fd=28))
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=5753,fd=6))
LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=5753,fd=7))
LISTEN 0      511                *:80              *:*    users:(("apache2",pid=15343,fd=4),("apache2",pid=15342,fd=4),("apache2",pid=15341,fd=4),("apache2",pid=15340,fd=4),("apache2",pid=15339,fd=4),("apache2",pid=15336,fd=4))
```

_Figure 1: Baseline services running (SSH/Apache/MariaDB) and listening ports (22/80/3306)_

**2.0.3 Baseline host-to-VM connectivity**

Connectivity to the VM was validated from the host system prior to rule changes. TCP reachability to
SSH (22) and HTTP (80) was confirmed (figure-2). This baseline ensures that later “blocked” results
can be attributed to the firewall configuration rather than service availability:

```powershell
PS C:\Users\HostComputer> Test-NetConnection 192.xxx.xx.x -Port 22

ComputerName     : 192.xxx.xx.x
RemoteAddress    : 192.xxx.xx.x
RemotePort       : 22
InterfaceAlias   : Wi-Fi
SourceAddress    : 192.xxx.xx.x
TcpTestSucceeded : True
```

```powershell
PS C:\Users\HostComputer> Test-NetConnection 192.xxx.xx.x -Port 80
ComputerName     : 192.xxx.xx.x
RemoteAddress    : 192.xxx.xx.x
RemotePort       : 80
InterfaceAlias   : Wi-Fi
SourceAddress    : 192.xxx.xx.x
TcpTestSucceeded : True
```

_Figure 2: Host-to-VM baseline connectivity confirmed (TCP/22 and TCP/80 reachable)_

---

#### **2.1 Task A - Reject connection on loopback interface**

The objective of this task was to configure the firewall to reject all traffic on the loopback
interface (lo). The loopback interface is used for local inter-process communication via the address
127.0.0.1. Blocking this interface demonstrates control over locally routed traffic and verifies
rule enforcement at the host level.

**2.1.1 Firewall Rule Configuration**

The following rules were inserted at the top of the INPUT and OUTPUT chains to reject traffic
entering and leaving the loopback interface.

```bash
sudo iptables -I INPUT 1 -i lo -j REJECT # Reject IN coming traffic
sudo iptables -I OUTPUT 1 -o lo -j REJECT # Reject OUT going traffic
```

The rules were verified using the line-numbers command (**figure 3**).

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -L -n -v --line-numbers

Chain INPUT (policy ACCEPT 65 packets, 12156 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 REJECT     all  --  lo     *       0.0.0.0/0            0.0.0.0/0            reject-with icmp-port-unreachable

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 33 packets, 3498 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 REJECT     all  --  *      lo      0.0.0.0/0            0.0.0.0/0            reject-with icmp-port-unreachable
```

_Figure 3: Loopback REJECT rules applied in INPUT and OUTPUT chains (lo)_

The output confirmed that REJECT rules were positioned at rule number 1 in both the INPUT and OUTPUT
chains.

**2.1.2 Validate Configuration**

To validate the configuration, an ICMP echo request was sent to the loopback address:

```bash
┌──(kali㉿kali)-[~]
└─$ ping -c 2 127.0.0.1

# Output: 100% packet loss => loopback is successfully blocked
PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.

--- 127.0.0.1 ping statistics ---
2 packets transmitted, 0 received, 100% packet loss, time 1029ms
```

_Figure 4: Loopback test fails — ping 127.0.0.1 blocked after REJECT rules_

The result showed (figure 4) **100% packet loss**, confirming that loopback traffic was successfully
blocked. Packet counters in the **iptables rule listing increased following the test**, verifying
that the REJECT rule was actively matching and processing traffic. This demonstrated that loopback
communication was effectively denied by the firewall.

**2.1.3 Restore Functionality**

The firewall configuration was restored to the previously saved baseline state (figure 5).

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables-restore < open-baseline.rules

# Test loopback again
┌──(kali㉿kali)-[~]
└─$ sudo iptables -S
-P INPUT ACCEPT
-P FORWARD ACCEPT
-P OUTPUT ACCEPT
```

_Figure 5: Baseline rollback point created (open-baseline.rules saved)_

After restoration, the loopback test was repeated:

```bash
┌──(kali㉿kali)-[~]
└─$ ping -c 2 127.0.0.1

PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.020 ms
64 bytes from 127.0.0.1: icmp_seq=2 ttl=64 time=0.031 ms

--- 127.0.0.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1026ms
rtt min/avg/max/mdev = 0.020/0.025/0.031/0.005 ms
```

_Figure 6: Loopback restored — ping 127.0.0.1 succeeds after baseline restore_

The result showed (figure 6) 0% packet loss, confirming that loopback functionality was successfully
restored.

**2.1.4 Results**

Task A successfully demonstrated that:

- Firewall rules can block traffic at the interface level.
- Loopback communication can be selectively denied.
- Rule effectiveness can be validated using packet counters and connectivity tests.
- Service functionality can be reliably restored using a controlled rollback procedure.

---

#### **2.2 Task B - Reject connection at port 22 for SSH**

The objective of this task was to configure the firewall to reject inbound SSH connections to the
virtual machine on TCP port 22. This demonstrates transport-layer access control for a specific
service while leaving other network functionality unaffected.

**2.2.1 Firewall Rule Configuration**

The following rule was inserted at the top of the INPUT chain to reject inbound SSH connections.

`sudo iptables -I INPUT 1 -p tcp --dport 22 -j REJECT --reject-with tcp-reset`

The rule was verified using `sudo iptables -L -n -v --line-numbers`

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -I INPUT 1 -p tcp --dport 22 -j REJECT --reject-with tcp-reset

# Match TCP when destination port is 22, then reject with TCP reset (sends RST to client to immediately close connection)
```

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -L -n -v --line-numbers

Chain INPUT (policy ACCEPT 11287 packets, 2131K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 REJECT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:22 reject-with tcp-reset

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 5764 packets, 606K bytes)
num   pkts bytes target     prot opt in     out     source               destination
```

_Figure 7: SSH REJECT rule applied for inbound TCP/22 (INPUT chain)_

**2.2.2 Validate Configuration**

Inbound SSH connectivity was tested from the host machine (figure 8). The baseline SSH connection
succeeded prior to applying the rule. After applying the rule the SSH connection failed, indicating
port 22 was blocked. Packet counters increased for the rule, confirming traffic matched the REJECT
rule.

```powershell
PS C:\Users\HostComputer> Test-NetConnection 192.xxx.xx.x -Port 22
WARNING: TCP connect to (192.xxx.xx.x : 22) failed

ComputerName           : 192.xxx.xx.x
RemoteAddress          : 192.xxx.xx.x
RemotePort             : 22
InterfaceAlias         : Wi-Fi
SourceAddress          : 192.xxx.xx.x
PingSucceeded          : True
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : False
```

_Figure 8: Host TCP/22 test fails (Test-NetConnection shows TcpTestSucceeded: False)_

**2.2.3 Restore Functionality**

Firewall state was restored to the baseline configuration: sudo iptables-restore <
open-baseline.rules

Figure-9 below, shows the SSH connectivity was retested and succeeded, confirming the rule was
removed and functionality restored.

```PowerShell
PS C:\Users\HostComputer> ssh kali@192.xxx.xx.x
kali@192.xxx.xx.x's password:
Linux kali 6.16.8+kali-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.16.8-1kali1 (2025-09-24) x86_64

The programs included with the Kali GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Thu Feb 19 02:21:54 2026 from 192.xxx.xx.x
┌──(kali㉿kali)-[~]
└─$
```

_Figure 9: SSH restored — host SSH login succeeds after baseline restore_

**2.2.4 Results**

Task B demonstrated that:

- SSH access can be selectively denied by filtering TCP port 22 in the INPUT chain.
- REJECT with TCP reset terminates connection attempts immediately.
- Normal connectivity can be reliably restored via baseline ruleset rollback.

---

#### **2.3 Task C - Deny ping and then demonstrate that you can restore ping command functionality**

The objective of this task was to deny ICMP echo-request packets (deny ping) to the virtual machine
and then restore ping functionality. This demonstrates protocol-based filtering at the network
layer.

**2.3.1 Firewall Rule Configuration**

The following rule was inserted (figure 10) at the top of the INPUT chain to drop inbound ICMP echo
requests.

`sudo iptables -I INPUT 1 -p icmp --icmp-type echo-request -j DROP`

The rule was verified using `sudo iptables -L -n -v --line-numbers`

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -I INPUT 1 -p icmp --icmp-type echo-request -j DROP

┌──(kali㉿kali)-[~]
└─$ sudo iptables -L -n -v --line-numbers

Chain INPUT (policy ACCEPT 1321 packets, 221K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 DROP       icmp --  *      *       0.0.0.0/0            0.0.0.0/0            icmptype 8

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 805 packets, 80050 bytes)
num   pkts bytes target     prot opt in     out     source               destination
```

_Figure 10: ICMP echo-request DROP rule applied (INPUT chain, icmptype 8)_

**2.3.2 Validate Configuration**

ICMP reachability was tested from the host machine. The Baseline ping succeeded prior to applying
the rule. After applying the rule, ping timed out (figure 11), indicating echo-requests were
silently dropped.

```PowerShell
PS C:\Users\HostComputer> ping 192.xxx.xx.x

Pinging 192.xxx.xx.x with 32 bytes of data:
Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.xxx.xx.x:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
```

_Figure 11: Host ping fails (ICMP timeouts) while DROP rule is active_

Packet counters increased (figure 12), confirming that echo-requests matched the DROP rule.

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -L -n -v --line-numbers

Chain INPUT (policy ACCEPT 1679 packets, 290K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        4   240 DROP       icmp --  *      *       0.0.0.0/0            0.0.0.0/0            icmptype 8

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 985 packets, 99130 bytes)
num   pkts bytes target     prot opt in     out     source               destination
```

_Figure 12: ICMP rule counters increment after ping test (DROP rule matched traffic)_

**2.3.3 Restore Functionality**

Firewall state was restored to the baseline configuration:

`sudo iptables-restore < open-baseline.rules`

Figure 13 shows the ping was retested on host computer and succeeded, confirming ICMP functionality
was restored.

```PowerShell
PS C:\Users\HostComputer> ping 192.xxx.xx.x

Pinging 192.xxx.xx.x with 32 bytes of data:
Reply from 192.xxx.xx.x: bytes=32 time<1ms TTL=64
Reply from 192.xxx.xx.x: bytes=32 time<1ms TTL=64
Reply from 192.xxx.xx.x: bytes=32 time<1ms TTL=64
Reply from 192.xxx.xx.x: bytes=32 time<1ms TTL=64

Ping statistics for 192.xxx.xx.x:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

_Figure 13: Ping restored — host receives replies after baseline restore_

**2.3.4 Results**

Task C demonstrated that:

- ICMP echo requests can be selectively blocked using protocol/type matching.
- DROP results in timeouts (no explicit rejection response).
- Baseline rollback restores network reachability.

---

#### **2.4 Task D - Reject all traffic coming to port 80**

The objective of this task was to reject inbound HTTP connections to the virtual machine on TCP
port 80. This demonstrates service-level access control to a web server while maintaining general
connectivity.

**2.4.1 Firewall Rule Configuration**

The following rule was inserted at the top of the INPUT chain (figure 14) to reject inbound HTTP
traffic:

`sudo iptables -I INPUT 1 -p tcp --dport 80 -j REJECT --reject-with tcp-reset`

The rule was verified using `sudo iptables -L -n -v --line-numbers`

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -I INPUT 1 -p tcp --dport 80 -j REJECT --reject-with tcp-reset
```

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -L -n -v --line-numbers
Chain INPUT (policy ACCEPT 7923 packets, 1488K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 REJECT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:80 reject-with tcp-reset

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 4014 packets, 429K bytes)
num   pkts bytes target     prot opt in     out     source               destination
```

_Figure 14: HTTP REJECT rule applied for inbound TCP/80 (INPUT chain)_

**2.4.2 Validate Configuration**

HTTP connectivity was tested from the host machine. The Baseline HTTP connection succeeded prior to
applying the rule. After applying the rule, the connection attempts failed, confirming port 80 was
blocked.

```PowerShell
PS C:\Users\HostComputer> Test-NetConnection 192.xxx.xx.x -Port 80
WARNING: TCP connect to (192.xxx.xx.x : 80) failed

ComputerName           : 192.xxx.xx.x
RemoteAddress          : 192.xxx.xx.x
RemotePort             : 80
InterfaceAlias         : Wi-Fi
SourceAddress          : 192.xxx.xx.x
PingSucceeded          : True
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : False
```

_Figure 15: Host HTTP connectivity fails after rule (curl/Test-NetConnection blocked)_

Moreover, the Packet counters increased (figure 16), confirming the rule was actively matching
traffic.

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -L -n -v --line-numbers
Chain INPUT (policy ACCEPT 8140 packets, 1527K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1       10   520 REJECT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:80 reject-with tcp-reset

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 4145 packets, 441K bytes)
num   pkts bytes target     prot opt in     out     source               destination
```

_Figure 16: HTTP rule counters increment after host test (REJECT rule matched traffic)_

**2.4.3 Restore Functionality**

Firewall state was restored to the baseline configuration:

`sudo iptables-restore < open-baseline.rules`

Figure 17 below shows the HTTP connectivity was retested and succeeded, confirming restoration.

```powershell
PS C:\Users\HostComputer> Test-NetConnection 192.xxx.xx.x -Port 80

ComputerName     : 192.xxx.xx.x
RemoteAddress    : 192.xxx.xx.x
RemotePort       : 80
InterfaceAlias   : Wi-Fi
SourceAddress    : 192.xxx.xx.x
TcpTestSucceeded : True
```

_Figure 17: HTTP restored — host TCP/80 test succeeds after baseline restore_

**2.4.4 Results**

Task demonstrated that:

- TCP port 80 can be selectively blocked using INPUT chain filtering.
- REJECT with TCP reset provides immediate connection failure feedback.
- Baseline rollback restores HTTP availability.

---

#### **2.5 Task E - Block incoming traffic connection to the IP address of your virtual machine**

The objective of this task was to block all incoming traffic destined for the virtual machine’s IP
address. This simulates host isolation by preventing all inbound communication regardless of
protocol or port.

**2.5.1 Firewall Rule Configuration**

The following rule was inserted at the top of the INPUT chain (figure 18) to drop all inbound
traffic destined for the VM’s IP. For the purposes of testing, the following IP address was used:

`sudo iptables -I INPUT 1 -d 192.xxx.xx.x -j DROP`

- `-d` = destination address
- If packet is going to 192.xxx.xx.x
- Then DROP it

The rule was verified using:

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -L -n -v --line-numbers
Chain INPUT (policy ACCEPT 1722 packets, 320K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        3   234 DROP       all  --  *      *       0.0.0.0/0            192.xxx.xx.x

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 884 packets, 102K bytes)
num   pkts bytes target     prot opt in     out     source               destination
```

_Figure 18: Destination-based DROP rule applied (block all inbound traffic to VM IP)_

**2.5.2 Validate Configuration**

Connectivity was tested from the host machine. Ping timed out (ICMP blocked by DROP rule) and TCP
port checks for 22 and 80 failed (figures 19 and 20). Packet counters increased (figure 21),
confirming the destination-based rule matched inbound traffic.

```powershell
PS C:\Users\HostComputer> ping 192.xxx.xx.x

Pinging 192.xxx.xx.x with 32 bytes of data:
Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.xxx.xx.x:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
```

_Figure 19: Host connectivity fails — ping and TCP tests time out during VM IP block – Port 22_

```powershell
PS C:\Users\HostComputer> Test-NetConnection 192.xxx.xx.x -Port 80
WARNING: TCP connect to (192.xxx.xx.x : 80) failed
WARNING: Ping to 192.xxx.xx.x failed with status: TimedOut

ComputerName           : 192.xxx.xx.x
RemoteAddress          : 192.xxx.xx.x
RemotePort             : 80
InterfaceAlias         : Wi-Fi
SourceAddress          : 192.xxx.xx.x
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : False
```

_Figure 20: Host connectivity fails — ping and TCP tests time out during VM IP block – Port 80_

> Because we used DROP, the ping test shows `PingSucceeded: False` with no response, and the TCP
> tests for SSH, HTTP, and MySQL all show `TcpTestSucceeded: False`, confirming that all inbound
> traffic to the VM’s IP address is effectively blocked by the firewall rule.

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -L -n -v --line-numbers
[sudo] password for kali:
Chain INPUT (policy ACCEPT 1989 packets, 402K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1      323 24418 DROP       all  --  *      *       0.0.0.0/0            192.xxx.xx.x

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 884 packets, 102K bytes)
num   pkts bytes target     prot opt in     out     source               destination
```

_Figure 21: Rule counters confirm inbound traffic dropped (DROP rule matched traffic)_

**2.5.3 Restore Functionality**

Firewall state was restored to the baseline configuration:

`sudo iptables-restore < open-baseline.rules`

Connectivity tests were repeated and succeeded (figures 22 and 23), confirming full restoration.

```bash
PS C:\Users\HostComputer> ping 192.xxx.xx.x

Pinging 192.xxx.xx.x with 32 bytes of data:
Reply from 192.xxx.xx.x: bytes=32 time<1ms TTL=64
Reply from 192.xxx.xx.x: bytes=32 time<1ms TTL=64
Reply from 192.xxx.xx.x: bytes=32 time<1ms TTL=64
Reply from 192.xxx.xx.x: bytes=32 time<1ms TTL=64

Ping statistics for 192.xxx.xx.x:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

_Figure 22: Connectivity restored — host ping check succeed after baseline restore_

```powershell
PS C:\Users\HostComputer> Test-NetConnection 192.xxx.xx.x -Port 22

ComputerName     : 192.xxx.xx.x
RemoteAddress    : 192.xxx.xx.x
RemotePort       : 22
InterfaceAlias   : Wi-Fi
SourceAddress    : 192.xxx.xx.x
TcpTestSucceeded : True

PS C:\Users\HostComputer> Test-NetConnection 192.xxx.xx.x -Port 80

ComputerName     : 192.xxx.xx.x
RemoteAddress    : 192.xxx.xx.x
RemotePort       : 80
InterfaceAlias   : Wi-Fi
SourceAddress    : 192.xxx.xx.x
TcpTestSucceeded : True
```

_Figure 23: Connectivity restored — host port checks succeed after baseline restore_

**2.5.4 Results**

Task E demonstrated that:

- Destination-based filtering can isolate a host from inbound network traffic.
- DROP results in timeouts for both ICMP and TCP.
- Rollback restores all inbound communications.

---

#### **2.6 Task F - Allow traffic coming to port 80 (inbound) but reject accessing IP address 8.8.8.8.**

The objective of this task was to allow inbound HTTP traffic to the VM (TCP port 80) while rejecting
outbound access from the VM to a specific destination IP address (8.8.8.8). This demonstrates
directional filtering using INPUT and OUTPUT chains.

**2.6.1 Firewall Rule Configuration**

The following rules were inserted to implement the required policy:

`sudo iptables -I INPUT 1 -p tcp --dport 80 -j ACCEPT # Allow inbound HTTP traffic`

`sudo iptables -I OUTPUT 1 -d 8.8.8.8 -j REJECT # Reject outbound traffic to 8.8.8.8`

The rules were verified using:

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -L -n -v --line-numbers
Chain INPUT (policy ACCEPT 1141 packets, 121K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:80

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 1005 packets, 85693 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 REJECT     all  --  *      *       0.0.0.0/0            8.8.8.8              reject-with icmp-port-unreachable
```

_Figure 24: Rules applied — INPUT allows TCP/80 and OUTPUT rejects destination 8.8.8.8_

**2.6.2 Validate Configuration**

Testing confirmed the intended directional behaviour. Inbound HTTP from the host (figure 25) to the
VM remained available (port 80 test succeeded). The Outbound connectivity from the VM to 8.8.8.8
failed (ping failed due to OUTPUT rule). In addition, the Packet Counters increased on both rules,
confirming traffic was matched.

Testing Inbound port 80 from host:

```bash
PS C:\Users\HostComputer> Test-NetConnection 192.xxx.xx.x -Port 80

ComputerName     : 192.xxx.xx.x
RemoteAddress    : 192.xxx.xx.x
RemotePort       : 80
InterfaceAlias   : Wi-Fi
SourceAddress    : 192.xxx.xx.x
TcpTestSucceeded : True
```

_Figure 25: Inbound HTTP remains reachable from host (TCP/80 succeeds while rules active)_

Figure 26 shows testing Outbound from Kali with a 100% packet loss:

```bash
┌──(kali㉿kali)-[~]
└─$ ping -c 2 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
From 192.xxx.xx.x icmp_seq=1 Destination Port Unreachable
ping: sendmsg: Operation not permitted
From 192.xxx.xx.x icmp_seq=2 Destination Port Unreachable
ping: sendmsg: Operation not permitted

--- 8.8.8.8 ping statistics ---
2 packets transmitted, 0 received, +2 errors, 100% packet loss, time 1005ms
```

_Figure 26: Outbound connectivity blocked — VM ping to 8.8.8.8 fails while OUTPUT rule active_

```bash
┌──(kali㉿kali)-[~]
└─$ sudo iptables -L -n -v --line-numbers
Chain INPUT (policy ACCEPT 1456 packets, 152K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        4   172 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:80

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 1292 packets, 112K bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        2   168 REJECT     all  --  *      *       0.0.0.0/0            8.8.8.8              reject-with icmp-port-unreachable
```

_Figure 27: Rule counters confirm both behaviours (HTTP allowed; 8.8.8.8 traffic rejected)_

**2.6.3 Restore Functionality**

Firewall state was restored to the baseline configuration:

`sudo iptables-restore < open-baseline.rules`

The following (figure 28) shows the Outbound connectivity to 8.8.8.8 was retested and succeeded,
confirming the OUTPUT restriction was removed.

```bash
┌──(kali㉿kali)-[~]
└─$ ping -c 2 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=58.6 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=117 time=47.0 ms

--- 8.8.8.8 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1003ms
rtt min/avg/max/mdev = 47.034/52.826/58.618/5.792 ms
```

_Figure 28: Outbound restored — VM ping to 8.8.8.8 succeeds after baseline restore_

**2.6.4 Results**

Task F demonstrated that:

- Inbound and outbound traffic can be controlled independently via INPUT and OUTPUT chains.
- Specific egress destinations can be blocked without affecting allowed inbound services.
- Rule effectiveness can be confirmed via connectivity tests and packet counters.

---
---

### **3. Testing Method and Validation Process**

This section describes the consistent methodology used to validate each firewall configuration in
Tasks A–F. Each configuration was treated as a controlled experiment, ensuring the observed outcomes
were attributable to firewall rule changes rather than unrelated system or network issues. Baseline
service availability, listening ports, and host-to-VM connectivity were validated prior to testing
(Ref: 2.0 Pre-Test Setup and Baseline Validation).

#### **3.1 Baseline Establishment**

Before applying any firewall rules, a baseline state was established to confirm that the system was
functioning normally:

- The default iptables policies were confirmed to be permissive (INPUT/OUTPUT/FORWARD set to
  ACCEPT), providing an open starting point.
- Required services were confirmed to be available where relevant (SSH for port 22 tests and Apache
  for port 80 tests).
- Connectivity between the host machine (Windows 11) and the virtual machine (Kali Linux) was
  validated to confirm the network path was functional prior to introducing firewall changes.

A baseline ruleset snapshot was saved using iptables-save, enabling reliable rollback to a known
working state after each experiment.

#### **3.2 Controlled Rule Deployment**

Firewall rules were applied using a consistent approach:

- Rules were inserted at the top of the relevant chain using `iptables -I … 1` to ensure rule
  precedence and to avoid being bypassed by any existing rules.
- Rules were applied to the appropriate direction of traffic:
  - `INPUT` chain for inbound filtering (blocking SSH/HTTP access to the VM)
  - `OUTPUT` chain for outbound filtering (blocking access from the VM to a specific destination IP)

After each insertion, the active ruleset was verified using rule listings with line numbers and
counters. This confirmed that the intended rule existed, was placed at the expected priority, and
matched the target traffic conditions of protocol, port, and destination.

#### **3.3 Practical Validation Testing**

Testing was performed using real traffic generated from the host machine and from the VM itself.
This ensured that results represented genuine, practical behaviour rather than theoretical
expectations.

**3.3.1 ICMP (Ping) Testing**

ICMP echo requests were used to validate network-layer reachability and ICMP filtering. When ICMP
was dropped or rejected by a rule, expected symptoms included timeouts or explicit error messages.
After rollback, successful ping responses confirmed restoration.

**3.3.2 TCP Port-Level Testing**

Transport-layer connectivity was validated using TCP connection testing to specific ports (22 for
SSH and 80 for HTTP). Host-based testing tools were used to determine whether a connection could be
established:

- A successful test indicated the service port was reachable and accepting connections.
- A failed test indicated that connections were blocked at the firewall layer (or that the service
  was not listening, which was controlled by verifying service status during baseline checks).

This approach enabled clear differentiation between **service not running** and **service running
but filtered by firewall rules**.

**3.3.3 Application-Level Testing**

Where appropriate, application-level testing was used to confirm service behaviour beyond simple
port reachability Such as using HTTP requests to validate web server access. This provided higher
confidence that services were reachable and functioning when allowed, and that access failures
aligned with firewall policy when blocked.

#### **3.4 Verification Using Packet Counters**

In addition to connectivity results, iptables packet counters were used as supporting evidence that
firewall rules were actively matching live traffic. After running each practical test, rule counters
were reviewed to confirm that:

- The relevant firewall rule was triggered by the test traffic, and
- The observed behaviour (success/failure) correlated with the rule target (ACCEPT/DROP/REJECT).

This strengthened the causal link between rule configuration and test outcomes.

#### **3.5 Restoration and Recovery Validation**

After each task, the firewall configuration was restored using the saved baseline ruleset snapshot
(iptables-restore). Restoration was validated by repeating the same tests performed prior to rule
application. Successful connectivity after restoration demonstrated that:

- The rule change was responsible for the observed blocking behaviour, and
- A controlled rollback process could reliably return the system to an operational state.

---
---


### **4. Efficient Management of iptables Rulesets**

Firewall rulesets become harder to manage as they grow, because rule order, redundancy, and outdated
entries can produce unintended behaviour or weaken security (NIST 2009). Firewall management
therefore includes not only initial configuration but also ongoing rule review, auditing, and
monitoring to keep policies effective and avoid conflicting or shadowed rules (Palo Alto Networks
n.d.a). In practice, these challenges are reduced by treating firewall policy as configuration code:
enforcing consistent rule structure, applying changes via repeatable scripts, documenting intent,
and using backups and version control to support safe rollback.

#### **4.1 Rule Ordering and Separation of Concerns**

iptables evaluates rules top-to-bottom, so ordering directly affects behaviour. A practical strategy
is to structure rules in logical groups (separation of concerns), similar to how software components
are organised. In general, more specific rules should be placed before broader rules to avoid
unintended shadowing.

- Baseline safety rules first: allow established/related traffic and required core services (if
  using default-deny).
- Service-specific rules next: SSH, HTTP, etc.
- Network/protocol-specific rules next: ICMP controls, specific destination blocks.
- Catch-all rule last: say, a final DROP (in a default-deny policy).

This reduces ambiguity and prevents unintended bypass. It also makes troubleshooting faster because
rule intent is predictable based on position.

#### **4.2 Backup, Rollback, and Change Control**

A key operational requirement is reliable rollback. Using iptables-save and iptables-restore
provides a snapshot/restore mechanism so changes can be reversed quickly if they break access. In
practice, saving a known-good baseline before modifications prevents “lockout” scenarios and
supports safe experimentation and recovery.

#### **4.3 Scripted Deployment (Repeatability)**

Manually entering iptables commands increases the chance of mistakes and inconsistent states. A more
efficient approach is to deploy rules via script such as “reset-firewall.sh” or “apply-firewall.sh”
so the same policy can be reproduced consistently across reboots or multiple systems. This is
equivalent to scripted deployment in application development where repeatability reduces
configuration drift and human error. A deployment script typically includes:

- flushing/resetting chains,
- applying rules in a defined order,
- and optionally saving the resulting ruleset.

#### **4.4 Rule Documentation and Comments**

As rulesets grow, it becomes difficult to understand “why” a rule exists (Common operational issue).
Commenting rules (where supported) and maintaining a short rule description list improves
maintainability and auditability. This is similar to code documentation where the goal is to
preserve intent so future changes don’t accidentally weaken security or break services. In practice,
this is a common pain point.

#### **4.5 Version Control and Configuration-as-Code**

iptables rules can be managed like software source code using version control (Git). Storing scripts
and saved rulesets in a repository provides:

- change history (who changed what and why),
- quick rollback to a previous known-good version,
- and easier review before deployment.

This Configuration-as-Code (CaC) for managing system settings and policies, approach aligns with
modern infrastructure practices and is directly comparable to maintaining a REST API or MERN stack
in Git. The firewall policy becomes a controlled artifact rather than an ad-hoc set of commands.

#### **4.6 Risk of Misconfiguration**

Firewall misconfiguration is a common operational risk. Common issues include:

- incorrect rule ordering,
- overly broad rules (blocking required services),
- forgetting rollback steps,
- and inconsistent rules across systems.

The controls described above (ordering, backups, scripts, comments, and version control) reduce
these risks by making the ruleset predictable, testable, and recoverable. These practices mirror
real-world software engineering/ development workflow (separation of concerns, scripted deployment,
documentation, and Git-based change control) but applied to firewall policy to reduce configuration
drift and misconfiguration risk.

---
---

### **5. Attacks on Packet Filtering Firewalls and Countermeasure Effectiveness**

Packet filtering firewalls control the flow of traffic by inspecting packet headers such as source
and destination IPs, protocols, and port numbers. While they serve as a foundational security tool,
they are vulnerable to certain attacks. The most common attacks against packet-filtering firewalls
include **IP spoofing**, **fragmentation-based evasion**, and **port scanning**. Although these
attacks exploit weaknesses in the firewall design, they can be mitigated through effective
countermeasures. The effectiveness of these countermeasures is context-dependent, and while the lab
work in this assessment demonstrates basic filtering techniques, industry best practices provide a
broader perspective on how to secure networks against these attacks.

#### **5.1 IP Spoofing and Source Routing**

IP spoofing occurs when an attacker forges the source IP address of packets to make them appear as
though they are from a trusted source. Source routing allows attackers to specify the path packets
should take, which can bypass security measures. These techniques exploit firewalls that rely on
source IP for access control. Possible counter measures are:

- **Anti-spoofing rules:** Drop inbound packets from internal/private address spaces on external
  interfaces.
- **Disable source routing:** Ensure that packets with source routing options are rejected.
- **Stateful inspection:** Track the connection state to verify the legitimacy of packets.

While **Task B - Reject SSH on port 22** demonstrated blocking based on known ports, IP spoofing is
harder to prevent using basic rules. Effective mitigation requires a combination of anti-spoofing
rules, stateful inspection, and ingress/egress filtering at the router level.

These countermeasures are effective at preventing most spoofing attacks, particularly from external
sources. However, if an attacker is already within the network or bypasses the firewall using tools
like source routing, these measures are less effective. So, while preventive controls like
anti-spoofing are important, additional security layers (IDS) are needed to defend against more
sophisticated attacks. **Task E - Block all inbound traffic to the VM IP address**, serves as a good
example of reducing the attack surface and denying external access altogether, preventing many types
of attacks from even reaching the firewall.

#### **5.2 Fragmentation-Based Evasion**

IP fragmentation can be used to evade packet filtering by splitting malicious packets into smaller
fragments, making it difficult for a firewall to inspect the complete packet. This method is often
used to bypass filters that focus only on complete packets (IETF 1995).

- **Fragment reassembly:** Ensure all fragments are reassembled before packet filtering occurs.
- **Dropping suspicious fragments:** Discard packets that do not meet fragmentation standards.
- **Stateful inspection:** Ensure firewalls track the state of the packet stream, which prevents
  evasion via fragmentation.

In the lab, we didn’t implement fragmentation evasion, but **Task C - Deny Ping** demonstrates how
filtering based on packet content (ICMP) can block certain types of network traffic. Fragmentation
evasion requires a more sophisticated approach, where packets are reassembled in a controlled state
before filtering occurs.

Stateful inspection is an effective countermeasure against this type of evasion. Modern firewalls
capable of deep packet inspection (DPI) can perform fragment reassembly and filter malicious
fragments. However, poorly configured or older firewalls may still be vulnerable to this attack,
especially if fragmentation handling is not adequately implemented.

#### **5.3 Port Scanning and Stateless Evasion Techniques**

Port scanning is a common technique used by attackers to discover open ports and services on a
target system. Techniques such as SYN scans, ACK scans, FIN scans, and Xmas scans are designed to
evade detection by simple stateless packet filters. Some counter measures can include:

- **Default-deny policy:** Use a default-deny rule that blocks all traffic except for explicitly
  allowed services. Demonstrated in **Task F - Allow inbound HTTP but reject access to 8.8.8.8**
  showing the use of filtering based on destination IP, allowing access to specific services while
  blocking unwanted outbound traffic.
- **Stateful inspection:** Modern firewalls that track connection states (via Conntrack or similar
  mechanisms) can detect attempts to bypass filters with unusual TCP flags.
- **Rate limiting and logging:** Detect scanning attempts by rate-limiting connections and logging
  anomalies to detect scanning attempts.
- **Intrusion Detection Systems (IDS):** Integrate IDS to detect scanning behaviour and raise alerts
  for suspicious activity.

While basic port scanning can be stopped by firewalls with default-deny policies, more sophisticated
techniques like fragmentation or stealth scanning may bypass simple packet filters. Stateful
inspection firewalls and rate-limiting measures significantly reduce the effectiveness of these
scans. However, advanced attackers can still employ stealthier methods or use fragmentation to evade
detection. IDS/IPS integration is the most effective countermeasure for this type of reconnaissance
attack. **Task E - Block incoming traffic to the VM IP address**, addressed this type of scanning by
simply blocking all traffic from external sources, reducing the attack surface entirely.


## Part B: Reflection

Defence-in-depth is a core cyber security concept where multiple security controls – physical,
technical, and administrative – work together to protect systems. Firewalls sit within the technical
layer and provide network boundary control, but this assessment reinforced that a firewall is not a
complete security solution on its own (Shanks and Duca n.d).

Firewalls act as a first line of defence by filtering traffic using IP addresses, ports, and
protocols (Palo Alto Networks n.d.a). In Part A, this was demonstrated through targeted filtering
(blocking SSH on TCP/22 and HTTP on TCP/80), protocol filtering (denying ICMP echo requests),
destination-based blocking (isolating the VM IP in Task E), and directional control (Task F allowing
inbound HTTP while blocking outbound access to 8.8.8.8). These tasks show that firewalls are
effective for reducing the externally visible attack surface and controlling traffic flow at the
network and transport layers. However, firewalls cannot inspect what is happening inside endpoints
(malicious processes running on a host), and they do not automatically protect against
application-layer threats or social engineering-based compromise (Shanks and Duca n.d).

This leads to the key defence-in-depth issue: countermeasures to firewall attacks may be ineffective
in practice if other layers fail. For example, if a rule is misconfigured, placed in the wrong
order, or an allowed service becomes the attack path (malicious traffic over permitted ports such as
80/443), packet filtering may not stop the threat. Likewise, if an attacker gains internal access
(insider threat or compromised host), perimeter filtering can be bypassed through internal
connections. Evasion techniques (such as fragmentation tricks or stealth scanning) can also reduce
the reliability of simple packet-filter rules, making monitoring and detection controls (IDS/IPS,
logging, alerting) critical to catch what the firewall does not (Shanks and Duca n.d; Palo Alto
Networks n.d.b).

A useful analogy is GitHub SSH key authentication. Even if network access is permitted on port 22,
GitHub still requires the correct SSH key (and optionally a passphrase) before access is granted.
This mirrors defence-in-depth: an “open port” (network layer) does not equal access without
authentication controls (application/access layer) (GitHub n.d).

Finally, the course discussions highlighted ethical tension around moving from purely preventative
controls to proactive/offensive practices (penetration testing). These activities can strengthen
defence-in-depth by finding weaknesses early, but they require clear rules of engagement and legal
authorisation to avoid privacy breaches or unintended disruption. Overall, firewalls are essential,
but their effectiveness depends on layered controls and disciplined management rather than any
single technical countermeasure (Shanks et al. n.d).

## Conclusion

This assessment demonstrated that iptables can be used to enforce practical packet filtering
policies by controlling traffic at the network and transport layers. Across Tasks A–F, rules were
successfully applied to reject loopback traffic, restrict inbound services (SSH/HTTP), deny ICMP
echo requests, isolate the host by destination IP filtering, and implement directional control by
allowing inbound HTTP while blocking outbound access to a specific external IP. Each configuration
was validated through real host-to-VM testing, rule verification, packet counters, and controlled
rollback to a known baseline.

These results reinforce the role of firewalls as an essential technical control for reducing attack
surface and shaping traffic flow. However, firewalls are not sufficient on their own. They cannot
inspect endpoint behaviour, they may be bypassed through misuse of allowed services, and they rely
on correct configuration and ongoing management. For this reason, effective security depends on
defence-in-depth, combining firewalls with monitoring (IDS/IPS), endpoint controls, authentication,
patching, and incident response processes.

Finally, modern organisations increasingly rely on proactive security activities such as penetration
testing to validate controls. These practices can strengthen defence-in-depth, but they also
highlight the need for clear ethical and legal rules of engagement to ensure testing remains
authorised, safe, and accountable.

## References

- GitHub n.d., Best practices for securing accounts, GitHub Docs, accessed 27 February 2026,
  https://docs.github.com/en/code-security/tutorials/implement-supply-chain-best-practices/securing-accounts
- Internet Engineering Task Force (IETF) 1995, RFC 1858: Security Considerations for IP Fragment
  Filtering, IETF, accessed 4 March 2026, https://datatracker.ietf.org/doc/html/rfc1858.
- Michael Kerrisk n.d., iptables(8) - Linux manual page, man7.org, accessed 27 February 2026,
  https://man7.org/linux/man-pages/man8/iptables.8.html
- Microsoft n.d., Test-NetConnection, Microsoft Learn, accessed 26 February 2026,
  https://learn.microsoft.com/en-us/powershell/module/nettcpip/test-netconnection?view=windowsserver2025-ps
- National Institute of Standards and Technology (2009) Guidelines on Firewalls and Firewall Policy
  (SP 800-41 Revision 1), NIST, accessed 4 March 2026, https://csrc.nist.gov/pubs/sp/800/41/r1/final
- Palo Alto Networks n.d.a, What Is Firewall Management?, Palo Alto Networks Cyberpedia, accessed 4
  March 2026, https://www.paloaltonetworks.com.au/cyberpedia/what-is-firewall-management
- Palo Alto Networks n.d.b, IPS vs. IDS vs. Firewall: What Are the Differences?, Palo Alto Networks
  Cyberpedia, accessed 2 March 2026,
  https://www.paloaltonetworks.com.au/cyberpedia/firewall-vs-ids-vs-ips
- Shanks, V. & Duca, S. n.d., Using firewalls [video recording], INTE2665 Introduction to Cyber
  Security, RMIT University, Melbourne, accessed 1 March 2026, Canvas.
- Shanks, V., Duca, S. and Storrar, M. n.d., Cybercrime [video recording], INTE2665 Introduction to
  Cyber Security, RMIT University, Melbourne, accessed 1 March 2026, Canvas.
