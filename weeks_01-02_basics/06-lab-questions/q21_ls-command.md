# 21. Advanced `ls` Usage

## 1. Question

**“Find some different ways of using `ls` command.”**
_(Hint: sort by date and size, in ascending and descending order)_

```bash
ls -Sl  # sort by size
ls -Slr # sort by size reverse (descending)
```

Sort by time:

```bash
ls -tl  # sort by modification time
ls -tlr # sort by modification time reverse (descending)
```

---

## 2. Bro! What’s that mean exactly?

Question is asking:

> “How can I list files in a directory in different orders so I can quickly find what I care about?”

The `ls` command is not just for _listing files_ - it’s for:

- Analysing directories
- Finding recent changes
- Identifying large files
- Spotting suspicious activity

---

## 3. Commands Used

```bash
ls -Sl
ls -Slr
ls -tl
ls -tlr
```

Common flags involved:

- `-l` → long listing format
- `-S` → sort by file size
- `-t` → sort by modification time
- `-r` → reverse order

---

## 4. Example Usage | Output

```bash
# Basic ls command where `S` flag is used to sort by file size
┌──(kali㉿kali)-[~]
└─$ ls -S
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos


# Sort by file size (largest → smallest)
┌──(kali㉿kali)-[~]
└─$ ls -Sl
total 32
drwxr-xr-x 7 kali kali 4096 Jan 25 00:12 Desktop
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Documents
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Downloads
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Music
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Pictures
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Public
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Templates
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Videos


# Sort by file size (smallest → largest)
┌──(kali㉿kali)-[~]
└─$ ls -Slr
total 32
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Videos
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Templates
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Public
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Pictures
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Music
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Downloads
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Documents
drwxr-xr-x 7 kali kali 4096 Jan 25 00:12 Desktop


# Sort by modification time (newest → oldest)
┌──(kali㉿kali)-[~]
└─$ ls -tl
total 32
drwxr-xr-x 7 kali kali 4096 Jan 25 00:12 Desktop
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Documents
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Downloads
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Music
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Pictures
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Public
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Templates
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Videos


# Sort by modification time (oldest → newest)
┌──(kali㉿kali)-[~]
└─$ ls -tlr
total 32
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Videos
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Templates
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Public
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Pictures
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Music
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Downloads
drwxr-xr-x 2 kali kali 4096 Jan 17 02:00 Documents
drwxr-xr-x 7 kali kali 4096 Jan 25 00:12 Desktop
```

---

## 5. Gotchas | Common Mistakes

- ❌ **Confusing size vs disk usage**
  - `ls -S` → file size
  - `du` → disk usage

- ❌ **Thinking `-r` always means descending**
  - `-r` simply reverses whatever sort you chose

- ❌ **Forgetting `-l`**
  - Without `-l`, sorting is less informative

- ❌ **Assuming time means creation time**
  - `ls -t` sorts by **modification time**, not creation

---

## 6. Why `ls` Matters in Security

`ls` sorting is frequently used in:

- Incident response
- Malware triage
- Log analysis
- Forensic review

Security analysts often ask:

- “What files changed most recently?”
- “Why is this file so large?”
- “What appeared here overnight?”

Sorting quickly exposes **anomalies**.

---

## 7. Key Points

**Various `ls` flags:**

- `ls` lists directory contents
- `-l` shows permissions, owner, size, and time
- `-S` sorts by **file size**
- `-t` sorts by **modification time**
- `-r` reverses sort order
- `ls -Sl` → largest files first
- `ls -tl` → most recently modified files first
- Used heavily in **forensics and incident response**
- Modification time ≠ creation time

**High-Value Exam Facts/Tip:**

If the question mentions _“largest files”_ → think **`ls -Sl`**
If it mentions _“recently modified”_ → think **`ls -tl`**

---

## 8. Discussion

The `ls` command is often underestimated. But is ecessential knowledge for not just sceurity
purposes, but general system administration and **navigation** though Linux system and directories.

In reality, it’s one of the **first commands run during an investigation**.
Before analysing logs or binaries, analysts look at:

- What’s there
- What changed recently
- What looks abnormal

Being able to sort output effectively saves time and highlights **suspicious patterns early**.
