# Linux Fundamentals — Day 03
**Date:** 2026-03-21  
**Source:** [LabEx Linux Fundamentals](https://labex.io/)  
**Topic:** File Contents and Comparing — cat, head, tail, diff, man

---

## cat — View File Contents
Displays the entire contents of a file directly in the terminal.

```bash
cat file.txt                  # print the full contents of a file
cat -n file.txt               # print contents with line numbers
cat file1.txt file2.txt       # print multiple files one after another
cat file1.txt file2.txt > combined.txt  # combine two files into one new file
```

Example output of `cat -n`:
```
     1	#!/bin/bash
     2	echo "Hello World"
     3	cd /home/oladapo
```

> `cat` is best for short files. For long files, use `less` instead — otherwise the output floods your terminal.

---

## head — View the Beginning of a File
Shows only the first part of a file. Default is the first 10 lines.

```bash
head file.txt                 # show first 10 lines (default)
head -n 20 file.txt           # show first 20 lines
head -n 5 file.txt            # show first 5 lines
head -c 100 file.txt          # show first 100 bytes instead of lines
```

> Useful for quickly checking what a file contains without opening the whole thing — especially large log files.

---

## tail — View the End of a File
Shows only the last part of a file. Default is the last 10 lines.

```bash
tail file.txt                 # show last 10 lines (default)
tail -n 20 file.txt           # show last 20 lines
tail -n 5 file.txt            # show last 5 lines
tail -c 100 file.txt          # show last 100 bytes
tail -f file.txt              # follow the file in real time — updates as new lines are added
```

> `tail -f` is one of the most useful commands in DevOps. You use it to **watch log files live** as an application runs — for example monitoring a deployment or debugging an error in real time.

---

## diff — Compare File Contents
Shows the line-by-line differences between two files.

```bash
diff file1.txt file2.txt          # compare two files
diff -u file1.txt file2.txt       # unified format — easier to read (shows context around changes)
diff -r dir1/ dir2/               # compare two entire directories recursively
```

Example output of `diff file1.txt file2.txt`:
```
2c2
< Hello World
---
> Hello Linux
```

Reading diff output:
- `<` = line from the first file
- `>` = line from the second file
- `c` = changed, `a` = added, `d` = deleted

Example output of `diff -u` (unified — more readable):
```
--- file1.txt
+++ file2.txt
@@ -1,3 +1,3 @@
 Line one
-Hello World
+Hello Linux
 Line three
```

> `-` lines are from file1 (removed). `+` lines are from file2 (added). Lines with no symbol are unchanged context.

**diff -r — Compare Directories:**
```bash
diff -r folder1/ folder2/        # show all differences between two directories
```

> This is useful in DevOps for spotting differences between environment configs — e.g. DEV vs PROD configuration folders.

---

## man — Read the Manual
Opens the full manual page for any Linux command. The most important command to know when you are stuck.

```bash
man cat                       # manual for cat
man diff                      # manual for diff
man ls                        # manual for ls
man man                       # the manual for the manual itself
```

**Navigating the man page:**

| Key | Action |
|-----|--------|
| `Space` or `f` | Scroll down one page |
| `b` | Scroll up one page |
| `q` | Quit and return to terminal |
| `/searchterm` | Search for a word within the manual |
| `n` | Jump to next search result |

> Every command you learn has a man page. When in doubt — `man <command>`. This is how experienced Linux engineers look things up too.

---

## Practical DevOps Uses — Why These Commands Matter

| Command | Real DevOps use case |
|---------|---------------------|
| `cat` | Quickly view config files, scripts, or log snippets |
| `cat -n` | View a script with line numbers to pinpoint an error |
| `head` | Check the top of a large log file or CSV |
| `tail -f` | Watch a deployment log or application output in real time |
| `diff` | Compare two versions of a config file before deploying |
| `diff -r` | Spot differences between DEV and PROD config directories |
| `man` | Look up any flag or option without leaving the terminal |

---

## LabEx Challenge Completed ✅
*"File Contents and Comparing" — cat, cat -n, head, tail, diff, diff -r, man*

---

*Next: File permissions (ls -l, chmod, chown), users and groups, grep and pipes*