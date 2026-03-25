# 16. Check Free Memory

## 1. Question

"Check which command to use to see free memory."

Command to show free memory in GB

`free -g`

Command to show free memory in MB

`free -m`

---

## 2. Bro! What’s that mean exactly?

Question is asking:

> “How much RAM does my system have, how much is currently being used, and how much is available?”

This question is **not** about disk space, and not about CPU — it’s specifically about **system memory (RAM)**.

---

## 3. Commands Used

```bash
# Check free memory in GB
free -g

# Check free memory in MB
free -m


# ---------- Not required by the lab, but useful context

# Check free memory in human-readable format
free -h


# ---------- Additional useful commands to check memory usage

# Check memory usage with 'vmstat' (alternative command)
vmstat -s

# Check memory usage with 'top' (real-time monitoring)
top

# Check memory usage with 'htop' (interactive monitoring, if installed)
htop

# Check memory usage with 'cat /proc/meminfo' (detailed info)
cat /proc/meminfo
```

---

## 4. Example Usage | Output


```bash

# Example output for 'free -g'
┌──(kali㉿kali)-[~]
└─$ free -g
               total        used        free      shared  buff/cache   available
Mem:               1           0           0           0           0           1
Swap:              0           0           0

# Example output for 'free -m'                                                                                 
┌──(kali㉿kali)-[~]
└─$ free -m
               total        used        free      shared  buff/cache   available
Mem:            1971         843         570          13         747        1127
Swap:            953           0         953

# Example output for 'free -h'                                                                                       
┌──(kali㉿kali)-[~]
└─$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       842Mi       571Mi        13Mi       747Mi       1.1Gi
Swap:          953Mi          0B       953Mi

```


---

## 5. Gotchas | Common Mistakes

- ❌ **Confusing “free” with “available”**
  - `free` = completely unused RAM
  - `available` = RAM that _can be used_ (includes cache)

- ❌ **Thinking Linux is “wasting memory”**
  - Linux aggressively uses RAM for caching (this is good)

- ❌ **Mixing up RAM and disk**
  - `free` → memory
  - `df` → disk space

- ❌ **Panicking when `free` is low**
  - Low `free` ≠ problem
  - Low `available` = potential problem

---

## 6. Why it Matters in Security

Memory usage is critical for:

- Detecting **resource exhaustion attacks**
- Identifying **malware or runaway processes**
- Investigating **denial-of-service (DoS)** conditions
- Understanding system stability during incidents

Attackers may:

- Intentionally exhaust memory
- Trigger crashes
- Hide malicious processes consuming RAM

Defenders monitor memory to spot **abnormal behaviour early**.

---

## 7. Key Points

**Some high-value exam facts/tips:**

- `free` = **show free memory**
More importantly: `free` shows memory usage overall (RAM and swap usage)
- `-m` = megabytes (MB) -> more detailed
- `-g` = gigabytes (GB) -> cleaner, high-level
- “Available” memory is more important than “free”
- Swap usage indicates memory pressure

---

## 8. Discussion

This question looks simple, but it teaches a **core Linux truth**:

> Unused memory is wasted memory.

Linux is designed to **use RAM aggressively** for caching to improve performance.
Only when memory is genuinely exhausted does the system start swapping or failing.

From a cyber security perspective, understanding memory usage helps distinguish between:

- Normal system behaviour
- Performance issues
- Active attacks or compromise

---
