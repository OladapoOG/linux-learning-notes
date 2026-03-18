# Linux Fundamentals — Day 01
**Date:** 2026-03-18  
**Source:** [LabEx Linux Fundamentals](https://labex.io/)  
**Topic:** Basic navigation and system commands

---

## pwd — Print Working Directory
Shows the full path of the directory you are currently in.

```bash
pwd
# Output example: /home/oladapo
```

> Think of it as "where am I right now?" in the file system.

---

## cd — Change Directory
Moves you from one directory to another.

```bash
cd Documents          # move into a folder called Documents
cd ..                 # go up one level to the parent directory
cd ~                  # go straight to your home directory
cd /                  # go to the root directory (top of the file system)
cd /home/oladapo      # go to an absolute path
```

> `~` always means your home directory. `..` always means one level up.

---

## whoami — Current User
Prints the username of the currently logged-in user.

```bash
whoami
# Output example: oladapo
```

> Useful when switching between users or working on shared systems.

---

## id — User Identity
Shows the user ID (UID), group ID (GID), and all groups the current user belongs to.

```bash
id
# Output example: uid=1000(oladapo) gid=1000(oladapo) groups=1000(oladapo),27(sudo)
```

> In DevOps, understanding user IDs and groups matters for file permissions and access control.

---

## id [username] — Identity of a Specific User
Shows the UID, GID and groups of any user on the system.

```bash
id root
# Output example: uid=0(root) gid=0(root) groups=0(root)
```

> `uid=0` means root — the superuser with full system access.

---

## cp — Copy Files and Directories
Copies a file or directory from one location to another.

```bash
cp file.txt backup.txt               # copy file.txt and name the copy backup.txt
cp file.txt /home/oladapo/Documents/ # copy file.txt into a different directory
cp -r myfolder/ myfolder_backup/     # copy an entire directory (-r means recursive)
```

> Always use `-r` when copying directories, otherwise the command will fail.

---

## echo — Print Text to the Terminal
Outputs a string of text to the terminal. Also used to write text into files.

```bash
echo "Hello World"               # prints: Hello World
echo "Hello" > file.txt          # writes "Hello" into file.txt (overwrites)
echo "Another line" >> file.txt  # appends "Another line" to file.txt
```

> `>` overwrites the file. `>>` appends to it without deleting existing content.

---

## rm — Remove Files and Directories
Deletes files or directories permanently. There is no recycle bin in Linux.

```bash
rm file.txt              # delete a single file
rm -r myfolder/          # delete a directory and everything inside it
rm -f file.txt           # force delete without confirmation prompt
rm -rf myfolder/         # force delete a directory and all contents — use carefully
```

> ⚠️ `rm -rf` is one of the most dangerous commands in Linux. Double-check your path before running it. There is no undo.

---

## Key Concepts from Day 01

| Concept | Meaning |
|---------|---------|
| Root directory `/` | The very top of the Linux file system — everything lives under it |
| Home directory `~` | Your personal folder, usually `/home/yourusername` |
| Absolute path | Full path from root e.g. `/home/oladapo/Documents` |
| Relative path | Path from where you currently are e.g. `../Documents` |
| Superuser (root) | User with UID 0 — full control of the system |

---

*Next: File permissions, mkdir, mv, ls flags*