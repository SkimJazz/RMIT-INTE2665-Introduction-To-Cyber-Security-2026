# 17. Monitor Processes with `top`

## 1. Question

“Try `top` command and discuss when this command should be used.”

---

## 2. Bro! What’s that mean exactly?

Question is asking:

> “What is happening on my system **right now**?”

The `top` command shows:

- Running processes
- CPU usage
- Memory usage
- Which processes are consuming resources
- All of this **live**, updating every few seconds

Think of `top` as:

> **Task Manager for Linux - but more powerful.**

This question is an exam favourite because it links **processes + CPU + memory + real-time monitoring**.

---

## 3. Commands Used

```bash
top
```

Common interactive keys inside `top` (not typed as commands):

- `q` → quit
- `P` → sort by CPU usage
- `M` → sort by memory usage
- `k` → kill a process (advanced / dangerous)
- `1` → show CPU usage per core

---

## 4. Example Usage | Output

Run:

```bash
top
```

```bash
# Output typical (but simplified):

# First few lines - Overall system summary
top - 14:22:01 up  2:35,  1 user,  load average: 0.25, 0.30, 0.28
Tasks: 212 total,   1 running, 211 sleeping

# CPU and Memory usage (consumption)
%Cpu(s):  3.2 us,  1.1 sy, 95.2 id
MiB Mem :   7933 total,   4210 free,   1542 used,   2180 buff/cache

# Then the list of processes (individual)
PID   USER      %CPU  %MEM   TIME+  COMMAND
1234  kali       8.2   2.1   0:32.45 firefox
8971  root       5.1   0.5   0:12.33 apache2
```

---

### How to read this (important)

- **Top section** → overall system health
- `%CPU` → CPU consumption per process
- `%MEM` → RAM usage per process
- **Bottom section** → individual processes

---

## 5. Gotchas | Common Mistakes

- ❌ **Thinking `top` shows historical data**
  - It only shows **current state**

- ❌ **Panicking over high CPU for a few seconds**
  - Short spikes are normal

- ❌ **Killing processes without understanding them**
  - You can crash your system

- ❌ **Confusing load average with CPU usage**
  - Load ≠ CPU percentage

---

## 6. Why it Matters in Security

`top` is often used during:

- Incident response
- Malware investigations
- Denial-of-Service detection
- System compromise analysis

Security teams use `top` to:

- Spot **runaway or hidden processes**
- Identify **unexpected CPU or memory usage**
- Detect **crypto-miners or backdoors**
- Confirm whether a system is under active stress

Attackers often leave **resource footprints** — `top` helps you see them.

---

## 7. Key Points

- `top` shows **real-time system activity**
- Displays **CPU, memory, and process usage**
- Updates automatically every few seconds
- Used for **live troubleshooting**, not historical analysis
- `%CPU` shows how much processing power a process is using
- `%MEM` shows how much RAM a process is consuming
- Load average reflects **system workload**, not just CPU
- Commonly used to detect **DoS attacks and malware**
- Similar concept to **Windows Task Manager**
- Quitting `top` does **not** stop processes

**Some high-value exam facts/tips:**

- `top` = **table of processes**
- Shows **real-time system stats**
- Key for **live monitoring**
- Interactive keys: `q`, `P`, `M`, `k`, `1`

**And**

If a question says _“real-time monitoring”_ → the answer is **`top`**

---

## 8. Discussion

`top` is one of the first commands run when _something feels wrong_.

It doesn’t fix problems - it **reveals** them.

From a cyber-security perspective, it helps answer questions like:

- “Why is this system slow?”
- “Is something abusing system resources?”
- “Did an attack just start?”

After learning `free` (memory snapshot), `top` adds **context and visibility**.
Together, they form a foundational **system triage toolkit**.

---
