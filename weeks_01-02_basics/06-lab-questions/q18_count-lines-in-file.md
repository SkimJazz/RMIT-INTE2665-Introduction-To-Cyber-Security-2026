# 18. Count Words and Lines in Files

## 1. Question

**“Try to count total words and lines in a file.”**
_(Hint: `wc`)_

---

## 2. Bro! What’s that mean exactly?

Linux is asking:

> “How big is this text file in terms of **lines**, **words**, and **characters**?”

This is **not** about file size in bytes (`ls -lh`) — it’s about **content size**.

The `wc` command helps you quickly understand:

- How many lines are in a file
- How many words it contains
- How much text you’re dealing with

---

## 3. Commands Used

```bash
wc file.txt
wc -l file.txt
wc -w file.txt

# ----- Variations of the `wc` command ----- #
wc -c file.txt
```

---

## 4. Example Usage | Output

Assume we have a file called `logExample.txt`.

Use `cat` to view the contents of logExample.txt:

```bash
┌──(kali㉿kali)-[~/Desktop]
└─$ cat logExample.txt
Jan 18 14:01:22 kali sshd[1023]: Accepted password for tom from 192.168.1.10 port 54321
Jan 18 14:02:01 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53112
Jan 18 14:02:45 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53113
Jan 18 14:03:10 kali sshd[1030]: Accepted password for kali from 192.168.1.20 port 60001
Jan 18 14:04:55 kali sudo[1042]: kali : TTY=pts/0 ; COMMAND=/usr/bin/apt update
```

```bash
# Count how many lines are in the file
┌──(kali㉿kali)-[~/Desktop]
└─$ wc -l logExample.txt

# Output:
5 logExample.txt


# Count how many words are in the file
┌──(kali㉿kali)-[~/Desktop]
└─$ wc -w logExample.txt

# Output:
67 logExample.txt


# Count how many characters are in the file
┌──(kali㉿kali)-[~/Desktop]
└─$ wc -c logExample.txt

# Output:
459 logExample.txt


# Count all (lines, words, characters) at once
┌──(kali㉿kali)-[~/Desktop]
└─$ wc logExample.txt

# Output:
5  67 459 logExample.txt



# ----- `wc` is often paired with ----- #

# `grep` to count specific lines matching a pattern
grep | wc -l


# Example:
# Find the phrase "Failed password" in logExample.txt and count how many times it appears
┌──(kali㉿kali)-[~/Desktop]
└─$ grep "Failed password" logExample.txt | wc -l

# Output:
2

# This counts security-relevant events - extremely common in practice.

```

---

## 5. Gotchas | Common Mistakes

- ❌ **Mixing up words and characters**
  - Words = space-separated tokens
  - Characters = every byte (including spaces and newlines)

- ❌ **Assuming `wc` shows file size**
  - It shows content counts, not disk usage

- ❌ **Forgetting input redirection**

  ```bash
  wc -l < logExample.txt

  # This removes the filename from output (sometimes required in scripts)
  ```

- ❌ **Counting binary files**
  - `wc` is meant for text files

---

## 6. Why `wc` Matters in Security

`wc` is heavily used in:

- Log analysis
- Incident response
- Data validation
- Evidence handling

Examples:

- “Did this log suddenly double in size?”
- “How many failed login attempts are recorded?”
- “Did my filtered output remove lines as expected?”

---

## 7. Key Points

- `wc` = **word count**
- Counts **lines, words, and characters**
- `-l` → lines
- `-w` → words
- `-c` → characters
- Output order is **always**: lines, words, characters
- Frequently used with `grep` and pipes
- Common in **log analysis and scripting**
- Fast way to measure **text data size**

**Some high-value exam facts/tips:**

If the question mentions _“counting entries in a file”_ → think **`wc -l`**

---

## 8. Discussion

`wc` is a deceptively powerful command.

On its own, it answers:

- “How big is this file logically?”

Combined with other commands, it answers:

- “How many events occurred?”
- “Did my filter work?”
- “Is this data abnormal?”

In cyber security, **counting is often the first sanity check** before deeper analysis.
If something suddenly changes in count, something _important_ probably happened.
