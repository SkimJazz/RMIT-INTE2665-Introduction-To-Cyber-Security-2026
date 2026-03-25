## 24. Folder Size Information

## 1. Question

**“Check how to check the total size of a particular folder or current folder.”**
_(Hint: `du -hs`)_

---

## 2. What does that mean exactly?

Question 24 is asking:

> “How much disk space is this directory (and everything inside it) actually using?”

This is about **directory-level disk usage**, not filesystem-level usage.

If `df` says “disk is full”, `du` answers:

> “Okay… _what_ is using the space?”

---

## 3. Commands Used

```bash
du -hs
du -hs folder_name
```

Common flags:

- `-h` → human-readable (KB, MB, GB)
- `-s` → summary (total only)

---

## 4. Example Usage | Output

![Image](https://ipcisco.com/wp-content/uploads/2022/09/LINUX-Disk-Usage-commands-ipcisco.png)

---

```bash
# Example 1: Check size of the **current directory**

┌──(kali㉿kali)-[~]
└─$ du -hs

# Output:
170M    .
# Meaning:
# Dot (.) represents current directory
# The current directory (and all subdirectories) uses 170 MB of disk space


# Example 2: Compare multiple directories (very useful)

┌──(kali㉿kali)-[~]
└─$ du -hs *

# Output:
1.5M    Desktop
4.0K    Documents
4.0K    Downloads
4.0K    Music
4.0K    Pictures
4.0K    Public
4.0K    Templates
4.0K    Videos

# This quickly shows **which folder is the biggest**.


# Example 3: Check size of a **specific folder**

┌──(kali㉿kali)-[~]
└─$ du -hs Documents

# Output:
4.0K    Documents
# Meaning: The 'Documents' folder (and all subdirectories) uses 4.0 KB of disk space
```

---

## 5. Gotchas | Common Mistakes

- ❌ **Forgetting `-s`**
  - Without `-s`, `du` lists every subdirectory (very noisy)

- ❌ **Confusing `du` with `df`**
  - `du` → directories/files
  - `df` → filesystems

- ❌ **Running `du` in `/` as root**
  - Can take a long time
  - Permission errors appear

- ❌ **Assuming `du` is instant**
  - Large directories take time to scan

---

## 6. Why it Matters in Security

`du` is used to:

- Investigate disk exhaustion incidents
- Identify suspicious large files
- Locate unexpected data growth
- Find attacker-dropped files or dumps

Attackers may:

- Drop large payloads
- Store stolen data
- Fill disks intentionally to disrupt logging

Defenders use `du` to:

- Regain disk space
- Preserve evidence
- Identify anomalies

---

## 7. Key Points

- `du` shows **disk usage by directory**
- `du -hs` gives a **clean summary**
- Used after `df` reports low disk space
- `-h` makes output readable
- `-s` prevents excessive output
- Helps identify **space-consuming folders**
- Common in **incident response and forensics**
- Complements `df`, not a replacement

**🔥 High-Value Exam Facts/Tip:**

If the question mentions _“which folder is using space”_ → think **`du -hs`**

---

## 8. Discussion

`du` turns a vague problem (“disk is full”) into an actionable one.

In cyber security, **visibility matters**:

- Full disks stop logs
- Missing logs mean blind investigations

Together:

- `df` finds the _problem_
- `du` finds the _cause_

This pairing is fundamental to both system administration and security operations.
