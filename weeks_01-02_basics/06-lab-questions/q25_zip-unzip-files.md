# 25. Zip and Unzip Files

## 1. Question

**“Check how to zip a file or multiple files into a single file.”**
_(Hint: use `zip` and `unzip`)_

---

## 2. Bro! What’s that mean exactly?

Question 25 is asking:

> “How can I compress one or more files into a single archive file, and then extract them later?”

This is about:

- **Compression**
- **Bundling files**
- **Storage and transfer efficiency**

You are _not_ encrypting files here — just compressing them.

---

## 3. Commands Used

```bash
zip filename.zip file.txt
zip filename.zip *.txt
unzip filename.zip
```

Optional but useful:

```bash
unzip -l filename.zip
```

---

## 4. Example Usage | Output

```bash
# Example 1: Zip a single file
┌──(kali㉿kali)-[~/Desktop/zipTest]
└─$ zip notes.zip notes.txt

# Output:
  adding: notes.txt (stored 0%)

# This is saying:
# Take the file notes.txt and compress it into notes.zip using `zip` format.
# The ziped file can be renamed to anything ending in .zip
# The (stored 0%) means the file was added without compression (likely because it's small).


# Example 2: Zip multiple files into one archive
┌──(kali㉿kali)-[~/Desktop/zipTest]
└─$ zip multipleFiles.zip log.txt reports.txt

# Output:
  adding: log.txt (stored 0%)
  adding: reports.txt (stored 0%)

# This is saying:
# Take the files log.txt and reports.txt and compress them into multipleFiles.zip using `zip` format.
# Again, the file can be renamed to anything ending in .zip
# The (stored 0%) means the files were added without compression (likely because they're small).


# Example 3: List contents without extracting (very useful)
┌──(kali㉿kali)-[~/Desktop/zipTest]
└─$ zip multipleFiles_1.zip *.txt

# Output:
  adding: log.txt (stored 0%)
  adding: notes.txt (stored 0%)
  adding: reports.txt (stored 0%)

# This is saying:
# Take all text files (*.txt) in the current directory and compress them into multipleFiles_1.zip using `zip` format.
# The (stored 0%) means the files were added without compression (YEP! coz they're small).


# Example 4: List contents without extracting (very useful)
┌──(kali㉿kali)-[~/Desktop/zipTest]
└─$ unzip -l multipleFiles_1.zip

# Output:
Archive:  multipleFiles_1.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
       24  2026-01-26 02:22   log.txt
       26  2026-01-26 02:23   notes.txt
       28  2026-01-26 02:24   reports.txt
---------                     -------
       78                     3 files

# This is saying:
# List the contents of multipleFiles_1.zip without extracting.
# It shows file sizes, modification dates, and names.
# Very useful to check what's inside before unzipping.


# Example 5: Unzip a file
┌──(kali㉿kali)-[~/Desktop/zipTest]
└─$ unzip multipleFiles.zip

# Output:
Archive:  multipleFiles.zip
replace log.txt? [y]es, [n]o, [A]ll, [N]one, [r]ename: r
new name: logUnziped.txt
 extracting: logUnziped.txt
replace reports.txt? [y]es, [n]o, [A]ll, [N]one, [r]ename: r
new name: reportsUnziped.txt
 extracting: reportsUnziped.txt

# This is saying:
# Extract the contents of multipleFiles.zip.
# If a file with the same name exists, it prompts for action (rename, overwrite, etc.).
# Here, files were renamed to avoid overwriting existing ones.
```

<!-- Following linkes are images that were removed from the original file -->
<!-- ![Image](https://www.cyberciti.biz/media/new/faq/2017/05/unzip-examples.jpg) -->

<!-- ![Image](https://cdn.educba.com/academy/wp-content/uploads/2020/11/Linux-Zip-Multiple-Files-3.jpg) -->

<!-- ![Image](https://media.geeksforgeeks.org/wp-content/uploads/20240117105108/unzip07.png) -->

---

## 5. Gotchas | Common Mistakes

- ❌ **Thinking zip = encryption**
  - Zip is compression only (unless password flags are used)

- ❌ **Forgetting wildcards**
  - `*.txt` means _all_ text files

- ❌ **Overwriting existing files when unzipping**
  - `unzip` will overwrite without warning

- ❌ **Zipping directories without `-r`**

  ```bash
  zip folder.zip myfolder     # ❌
  zip -r folder.zip myfolder  # ✅
  ```

---

## 6. Why it Matters in Security

Compression is used for:

- Evidence collection
- Log bundling
- File transfer
- Backups

In security operations:

- Logs are often zipped before transfer
- Malware samples may be zipped
- Incident data is archived for analysis

Attackers also:

- Zip stolen data before exfiltration

Knowing how archives work is essential on **both sides**.

---

## 7. Key Points

- `zip` compresses files into an archive
- `unzip` extracts archived files
- Multiple files can be zipped together
- Wildcards (`*`) allow bulk selection
- `unzip -l` lists contents safely
- Zip ≠ encryption
- Common format for **data transfer**
- Frequently used in **incident response**

**🔥 High-Value Exam Facts/Tip:**

If a question mentions _“compress multiple files”_ → think **`zip *.txt`**

---

## 8. Discussion

Zipping files is one of those skills that feels basic — until you’re in the middle of an investigation and need to:

- Package logs
- Preserve file integrity
- Transfer data cleanly

This question reinforces:

- File handling
- Command-line efficiency
- Safe data management

It also sets you up nicely for later topics like:

- Secure transfer
- Evidence handling
- Archiving during incidents
