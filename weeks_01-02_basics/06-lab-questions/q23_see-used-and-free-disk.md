# 23. Disk Usage Information

## 1. Question

**“Check how to use and free disk space.”**
_(Hint: `df`)_

---

## 2. What does that mean exactly?

Question 23 is asking:

> “How much disk space do I have, how much is used, and how much is still available?”

This question is about **storage (disk)**, not memory (RAM).
It answers:

- “Am I running out of space?”
- “Which filesystem is full?”
- “Can this system still write files?”

---

## 3. Commands Used

```bash
df
df -h
```

Related (context only, not required by the lab):

```bash
du
```

---

## 4. Example Usage | Output

![Image](https://www.linuxtechi.com/wp-content/uploads/2017/01/df-command-output-human-readable-format-1.jpg)

![Image](https://ipcisco.com/wp-content/uploads/2022/09/LINUX-Disk-Usage-commands-ipcisco.png)

![Image](https://opensource.com/sites/default/files/uploads/df-ha.png)

```bash
# Basic disk usage
┌──(kali㉿kali)-[~]
└─$ df

# Output:
Filesystem     1K-blocks     Used Available Use% Mounted on
udev              903224        0    903224   0% /dev
tmpfs             201844      980    200864   1% /run
/dev/sda1       82083148 16823204  61044396  22% /
tmpfs            1009208        4   1009204   1% /dev/shm
none                1024        0      1024   0% /run/credentials/systemd-journald.service
tmpfs            1009208        8   1009200   1% /tmp
none                1024        0      1024   0% /run/credentials/getty@tty1.service
tmpfs             201840      116    201724   1% /run/user/1000


# Human-readable format (recommended)
┌──(kali㉿kali)-[~]
└─$ df -h

# Output:
Filesystem      Size  Used Avail Use% Mounted on
udev            883M     0  883M   0% /dev
tmpfs           198M  980K  197M   1% /run
/dev/sda1        79G   17G   59G  22% /
tmpfs           986M  4.0K  986M   1% /dev/shm
none            1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs           986M  8.0K  986M   1% /tmp
none            1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
tmpfs           198M  116K  197M   1% /run/user/1000
```

---

### How to read this (important)

- **Size** → total disk size
- **Used** → space already used
- **Avail** → free space remaining
- **Use%** → how full the disk is
- **Mounted on** → where the filesystem is attached

---

## 5. Gotchas | Common Mistakes

- ❌ **Confusing disk space with memory**
  - `df` → disk
  - `free` → RAM

- ❌ **Panicking over tmpfs**
  - `tmpfs` is RAM-backed, not disk

- ❌ **Ignoring the Use% column**
  - This is often the most important value

- ❌ **Thinking `df` shows file sizes**
  - It shows filesystem usage, not individual files

---

## 6. Why it Matters in Security

Disk space exhaustion can:

- Crash services
- Prevent logs from being written
- Cause denial-of-service conditions
- Hide attacker activity (logs stop recording)

Attackers may:

- Intentionally fill disks
- Exploit systems that fail when storage is exhausted

Defenders monitor disk usage to ensure:

- Logs are retained
- Systems remain operational
- Evidence is preserved

---

## 7. Key Points

- `df` displays **filesystem disk usage**
- `df -h` shows output in **human-readable format**
- Shows **total, used, available space**
- Displays **mount points**
- Used to detect **full disks**
- Disk full ≠ memory full
- Common tool in **system monitoring**
- Frequently used during **incident response**

**🔥 High-Value Exam Facts/Tip:**

If the question mentions _“disk space”_ → the answer is **`df -h`**

---

## 8. Discussion

`df` is one of the first commands run when:

- A system behaves strangely
- Services stop working
- Logs suddenly stop updating

In cyber security, losing disk space can mean losing **visibility**.
No logs = no evidence.

This command complements:

- `free` (memory)
- `top` (processes)
- `ls` / `du` (files -> next: question 24)

Together, they give you a **full picture of system health**.
