# 22. Search for Strings in Files

## 1. Question

**“Find some string from a text file.”**
_(Hint: use `cat` and `grep`)_

---

## 2. Bro! What’s that mean exactly?

Question 22 is asking:

> “How can I search a text file and extract only the lines that contain a specific word or pattern?”

This is about **filtering information**, not just viewing it.

Instead of reading an entire file manually, `grep` lets you:

- Search for keywords
- Identify events
- Extract only what matters

And `cat` is used to display the file contents, which can then be piped into `grep` for filtering.

---

## 3. Commands Used

```bash
cat logExample.txt
grep "string" logExample.txt
cat logExample.txt | grep "string"
```

Common variations:

```bash
grep -i "string" logExample.txt
grep -n "string" logExample.txt
```

---

## 4. Example Usage | Output

```bash
cat file.txt | grep "search_term"
```

First up. Use `grep --help` to see all options.
```bash
# grep flags and options
┌──(kali㉿kali)-[~]
└─$ grep --help

Usage: grep [OPTION]... PATTERNS [FILE]...
Search for PATTERNS in each FILE.
Example: grep -i 'hello world' menu.h main.c
PATTERNS can contain multiple patterns separated by newlines.

Pattern selection and interpretation:
  -E, --extended-regexp     PATTERNS are extended regular expressions
  -F, --fixed-strings       PATTERNS are strings
  -G, --basic-regexp        PATTERNS are basic regular expressions
  -P, --perl-regexp         PATTERNS are Perl regular expressions
  -e, --regexp=PATTERNS     use PATTERNS for matching
  -f, --file=FILE           take PATTERNS from FILE
  -i, --ignore-case         ignore case distinctions in patterns and data
      --no-ignore-case      do not ignore case distinctions (default)
  -w, --word-regexp         match only whole words
  -x, --line-regexp         match only whole lines
  -z, --null-data           a data line ends in 0 byte, not newline

Miscellaneous:
  -s, --no-messages         suppress error messages
  -v, --invert-match        select non-matching lines
  -V, --version             display version information and exit
      --help                display this help text and exit

Output control:
  -m, --max-count=NUM       stop after NUM selected lines
  -b, --byte-offset         print the byte offset with output lines
  -n, --line-number         print line number with output lines
      --line-buffered       flush output on every line
  -H, --with-filename       print file name with output lines
  -h, --no-filename         suppress the file name prefix on output
      --label=LABEL         use LABEL as the standard input file name prefix
  -o, --only-matching       show only nonempty parts of lines that match
  -q, --quiet, --silent     suppress all normal output
      --binary-files=TYPE   assume that binary files are TYPE;
                            TYPE is 'binary', 'text', or 'without-match'
  -a, --text                equivalent to --binary-files=text
  -I                        equivalent to --binary-files=without-match
  -d, --directories=ACTION  how to handle directories;
                            ACTION is 'read', 'recurse', or 'skip'
  -D, --devices=ACTION      how to handle devices, FIFOs and sockets;
                            ACTION is 'read' or 'skip'
  -r, --recursive           like --directories=recurse
  -R, --dereference-recursive  likewise, but follow all symlinks
      --include=GLOB        search only files that match GLOB (a file pattern)
      --exclude=GLOB        skip files that match GLOB
      --exclude-from=FILE   skip files that match any file pattern from FILE
      --exclude-dir=GLOB    skip directories that match GLOB
  -L, --files-without-match  print only names of FILEs with no selected lines
  -l, --files-with-matches  print only names of FILEs with selected lines
  -c, --count               print only a count of selected lines per FILE
  -T, --initial-tab         make tabs line up (if needed)
  -Z, --null                print 0 byte after FILE name
```

![Image](https://phoenixnap.com/kb/wp-content/uploads/2024/02/multiple-file-search-grep.png)

```bash
# View logExample entire contents
┌──(kali㉿kali)-[~/Desktop]
└─$ cat logExample
# Output:
Jan 18 14:01:22 kali sshd[1023]: Accepted password for tom from 192.168.1.10 port 54321
Jan 18 14:02:01 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53112
Jan 18 14:02:45 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53113
Jan 18 14:03:10 kali sshd[1030]: Accepted password for kali from 192.168.1.20 port 60001
Jan 18 14:04:55 kali sudo[1042]: kali : TTY=pts/0 ; COMMAND=/usr/bin/apt update


# Find a specific string (e.g. failed logins)
┌──(kali㉿kali)-[~/Desktop]
└─$ grep "Failed password" logExample
# Output:
Jan 18 14:02:01 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53112
Jan 18 14:02:45 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53113


# Using `cat` with `grep` (as hinted in the lab)
┌──(kali㉿kali)-[~/Desktop]
└─$ cat logExample | grep "Failed password"
# Output:
Jan 18 14:02:01 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53112
Jan 18 14:02:45 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53113


# Case-insensitive search
┌──(kali㉿kali)-[~/Desktop]
└─$ grep -i "failed" logExample
Jan 18 14:02:01 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53112
Jan 18 14:02:45 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53113


# Show line numbers with matches
┌──(kali㉿kali)-[~/Desktop]
└─$ grep -n "Failed password" logExample
# Output:
2:Jan 18 14:02:01 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53112
3:Jan 18 14:02:45 kali sshd[1025]: Failed password for invalid user admin from 192.168.1.15 port 53113
```

---

## 5. Gotchas / Common Mistakes

- ❌ **Forgetting case sensitivity**
  - `grep` is case-sensitive by default

- ❌ **Searching for partial strings unintentionally**
  - `"Fail"` ≠ `"Failed"`

- ❌ **Using `cat | grep` unnecessarily**
  - `grep file.txt` is usually enough

- ❌ **Forgetting quotes for multi-word strings**

  ```bash
  grep Failed password log.txt   # ❌ wrong
  grep "Failed password" log.txt # ✅ correct
  ```

---

## 6. Why `grep` and `cat` Matter in Security

`grep` is one of the **most-used tools in cyber security**.
`cat` is often used to view files before or after filtering.
Combined, they help analysts quickly find relevant information in large log files.

They are used to:

- Find failed login attempts -> **spot brute-force attacks**
- Search for specific error messages -> **diagnose issues**
- Identify configuration changes -> **track unauthorized modifications**
- Analyze network traffic logs -> **detect anomalies**
- Detect suspicious commands -> **investigate potential intrusions**
- Extract indicators of compromise (IoCs) from logs -> **hunt threats**
- Filter logs during incident response -> **speed up investigations**

Example:

```bash
grep "Failed password" auth.log
```

This is **real-world SOC behaviour**, not just a lab exercise.

---

## 7. Key Points

- `grep` searches for **strings or patterns** in text
- Commonly used with **log files**
- Case-sensitive by default
- `-i` → ignore case
- `-n` → show line numbers
- Can be combined with pipes (`|`)
- Frequently paired with `wc -l`
- Used heavily in **incident response and log analysis**

**🔥 High-Value Exam Facts/Tip:**

If a question mentions _“searching logs for events”_ → the answer is **`grep`**

---

## 8. Discussion

`grep` is the backbone of text analysis in Linux.

On its own, it finds **what matters**.
Combined with `wc`, it answers **how often it happened**.
Combined with other tools, it becomes a **powerful investigation pipeline**.

This is exactly why Question 22 naturally follows Question 18 — together they form a **core security workflow**.
