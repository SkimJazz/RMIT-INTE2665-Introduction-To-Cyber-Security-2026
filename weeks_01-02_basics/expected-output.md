
# Weeks 1–2 — Expected Outputs & Assessment Notes

**INTE2665: Introduction to Cyber Security**

> ⚠️ **Important for Assessments**
> Linux command outputs **vary slightly** between systems.
> Your answers should focus on:
>
> * Structure
> * Key fields
> * Correct interpretation
>   Not exact character-for-character matching.

---

## 1. `useradd` and `passwd`

### Command

```bash
sudo useradd -m tom -s /bin/bash
sudo passwd tom
```

### Expected Output

```text
New password:
Retype new password:
passwd: password updated successfully
```

### Assessment Notes

* `-m` creates home directory `/home/tom`
* Shell assigned: `/bin/bash`
* No output from `useradd` indicates success

---

## 2. `su - tom`

### Command

```bash
su - tom
```

### Expected Output

```text
tom@kali:~$
```

### Assessment Notes

* Prompt changes from `root@kali` to `tom@kali`
* Confirms successful authentication and environment switch

---

## 3. `ps -ef | more`

### Command

```bash
ps -ef | more
```

### Expected Output (Partial)

```text
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 Jan15 ?        00:00:02 /sbin/init
root         2     0  0 Jan15 ?        00:00:00 [kthreadd]
```

### Assessment Notes

* **PID 1** is usually the first process (`systemd` or `init`)
* Older start times = long-running services
* Newer timestamps = recently launched processes

---

## 4. `service apache2 start/stop`

### Commands

```bash
sudo service apache2 start
sudo service apache2 stop
```

### Expected Output

```text
Starting Apache httpd web server: apache2
Stopping Apache httpd web server: apache2
```

(or sometimes **no output**)

### Assessment Notes

* Apache service is independent of SSH/MySQL
* Lack of SSH/MySQL messages is **expected**
* Services are managed individually via `systemd`

---

## 5. `/etc/resolv.conf`

### Command

```bash
cat /etc/resolv.conf
```

### Expected Output

```text
nameserver 192.168.1.1
```

(or public DNS like `8.8.8.8`)

### Assessment Notes

* Lists DNS servers
* Used for hostname-to-IP resolution
* Common attack vector (DNS poisoning)

---

## 6. `ifconfig` and `hostname`

### Commands

```bash
ifconfig
hostname
```

### Expected Output (Partial)

```text
eth0: inet 192.168.1.105
```

```text
kali
```

### Assessment Notes

* IP address confirms network connectivity
* Hostname uniquely identifies the system on the network

---

## 7. `ping rmit.edu.au`

### Command

```bash
ping rmit.edu.au
```

### Expected Output

```text
64 bytes from xxx.xxx.xxx.xxx: icmp_seq=1 ttl=54 time=23 ms
```

### Assessment Notes

* Successful replies indicate network reachability
* Uses ICMP protocol
* Failure may indicate firewall or DNS issues

---

## 8. `cp` and `mv`

### Commands

```bash
cp file1 file2
mv file2 file3
```

### Expected Output

```text
(no output)
```

### Assessment Notes

* Silent success is normal
* Errors appear only if files or permissions are incorrect

---

## 9. `scp`

### Command

```bash
scp file.txt user@10.10.0.2:/remote/directory
```

### Expected Output

```text
file.txt                          100%   12KB   1.2MB/s   00:01
```

### Assessment Notes

* Uses SSH for encrypted transfer
* Password prompt or SSH key authentication expected

---

## 10. `netstat -r`

### Command

```bash
netstat -r
```

### Expected Output (Partial)

```text
Destination     Gateway         Genmask         Iface
default         192.168.1.1     0.0.0.0         eth0
```

### Assessment Notes

* Default gateway routes traffic outside local network
* Critical for internet access

---

## 11. `dig rmit.edu.au`

### Command

```bash
dig rmit.edu.au
```

### Expected Output (Partial)

```text
ANSWER SECTION:
rmit.edu.au.     300   IN   A   131.170.xxx.xxx
```

### Assessment Notes

* Shows DNS resolution results
* A record maps domain to IP

---

## 12. `/etc/services`

### Command

```bash
cat /etc/services
```

### Expected Output

```text
ssh     22/tcp
http    80/tcp
https   443/tcp
mysql   3306/tcp
```

### Assessment Notes

* File maps services to ports
* Used by applications, not a live status list

---

## 14. Lock / Unlock User

### Commands

```bash
sudo passwd -l tom
sudo passwd -u tom
```

### Expected Output

```text
passwd: password expiry information changed
```

### Assessment Notes

* Locked user cannot log in
* Used for incident response and access control

---

## 16. `free -m`

### Command

```bash
free -m
```

### Expected Output

```text
              total        used        free
Mem:           3932         812        3120
```

### Assessment Notes

* Used to detect memory exhaustion
* Important for DoS detection

---

## 17. `top`

### Command

```bash
top
```

### Expected Output

* Live updating process list
* CPU and memory usage percentages

### Assessment Notes

* Used for real-time system monitoring
* Identifies runaway processes or malware

---

## 18. `wc`

### Commands

```bash
wc -l file.txt
wc -w file.txt
```

### Expected Output

```text
25 file.txt
120 file.txt
```

### Assessment Notes

* Common for log analysis
* Helps quantify data quickly

---

## 19. `whois rmit.edu.au`

### Command

```bash
whois rmit.edu.au
```

### Expected Output (Partial)

```text
Registrant: Royal Melbourne Institute of Technology
Country: AU
```

### Assessment Notes

* Reveals ownership and registrar info
* Useful for reconnaissance

---

## 23. `df -h`

### Command

```bash
df -h
```

### Expected Output

```text
Filesystem      Size  Used Avail Use%
/dev/sda1        40G   12G   26G  32%
```

### Assessment Notes

* Detects disk exhaustion
* Disk full = service failure risk

---

## 28. Port Usage (SSH Example)

### Command

```bash
netstat -tulpn | grep :22
```

### Expected Output

```text
tcp   0   0 0.0.0.0:22   LISTEN   1234/sshd
```

### Assessment Notes

* Confirms SSH service is active
* Identifies owning process

---

## 30. `vim`

### Command

```bash
vim filename
```

### Expected Output

* Terminal-based text editor opens
* No output until user interaction

### Assessment Notes

* Required skill for editing configs
* Essential for Linux administration

---

## 31. System Hardening (Discussion)

### Expected Answer Characteristics

✔ Mentions **firewalls**
✔ Mentions **SSH hardening**
✔ Mentions **account lockout**
✔ Mentions **strong passwords**

### Assessment Tip

Markers are checking **security reasoning**, not commands here.

---

## Marker-Friendly Summary Line (Use This)

> “Command outputs may vary slightly depending on system configuration; interpretations are based on standard Kali Linux behaviour.”

---


