# Linux Fundamentals — Day 02
**Date:** 2026-03-19  
**Source:** [LabEx Linux Fundamentals](https://labex.io/)  
**Topic:** Files and Directories — navigation, creation, copying, moving, removing

---

## Revisited: cd and pwd

```bash
pwd                        # print current directory
cd /home/oladapo           # move to an absolute path
cd ..                      # move up one level
cd ~                       # go to home directory
cd -                       # go back to the previous directory
```

> `cd -` is a handy shortcut — it toggles between your last two locations.

---

## touch — Create an Empty File
Creates a new empty file. If the file already exists, it just updates its timestamp.

```bash
touch notes.txt                  # create a single empty file
touch file1.txt file2.txt        # create multiple files at once
```

> ⚠️ `touch` does not exist in PowerShell by default. Use `New-Item -ItemType File -Path "filename"` on Windows instead.

---

## mkdir — Make a New Directory
Creates one or more new directories.

```bash
mkdir myfolder                   # create a single folder
mkdir folder1 folder2            # create multiple folders at once
mkdir -p parent/child/grandchild # create nested directories in one go (-p = parents)
```

> `-p` is very useful — without it, mkdir will fail if the parent folder doesn't exist yet.

---

## ls — List Directory Contents
Shows what is inside a directory.

```bash
ls                    # basic list of files and folders
ls -l                 # long format — shows permissions, owner, size, date
ls -a                 # show all files including hidden ones (starting with .)
ls -la                # combine both — long format + hidden files
ls -lh                # long format with human-readable file sizes (KB, MB)
ls /etc               # list contents of a specific directory
```

Example output of `ls -la`:
```
drwxr-xr-x  2 oladapo oladapo 4096 Mar 19 09:00 Documents
-rw-r--r--  1 oladapo oladapo  220 Mar 19 08:55 notes.txt
```

> The first character tells you the type: `d` = directory, `-` = regular file, `l` = symbolic link.

---

## cp — Copy Files and Directories
Duplicates a file or directory to a new location.

```bash
cp file.txt backup.txt                  # copy and rename in the same folder
cp file.txt /home/oladapo/Documents/    # copy to a different directory
cp -r myfolder/ myfolder_backup/        # copy an entire directory (-r = recursive)
cp -i file.txt backup.txt               # prompt before overwriting (-i = interactive)
```

> Always use `-r` when copying directories. Without it the command fails on folders.

---

## mv — Move or Rename Files and Directories
Moves a file to a new location, or renames it if you keep it in the same directory.

```bash
mv file.txt /home/oladapo/Documents/    # move file to a different directory
mv oldname.txt newname.txt              # rename a file (same directory)
mv myfolder/ /tmp/                      # move an entire directory
mv -i file.txt backup.txt              # prompt before overwriting
```

> Unlike `cp`, `mv` does not keep the original. The file is gone from its old location.

---

## rm — Remove Files
Permanently deletes files. No recycle bin — this is final.

```bash
rm file.txt               # delete a single file
rm file1.txt file2.txt    # delete multiple files
rm -i file.txt            # prompt for confirmation before deleting
rm -f file.txt            # force delete — no prompt, no error if file missing
rm -r myfolder/           # delete a directory and all its contents
rm -rf myfolder/          # force delete a directory — use with extreme caution
```

> ⚠️ `rm -rf` on the wrong path can delete critical system files. Always double-check your path first.

---

## rmdir — Remove an Empty Directory
Removes a directory, but only if it is completely empty.

```bash
rmdir myfolder            # removes myfolder only if it has nothing inside
rmdir -p parent/child     # removes child then parent if both are empty
```

> If the folder has any files in it, `rmdir` will fail. Use `rm -r` instead to remove a directory with contents.

---

## rmdir vs rm -r — When to Use Which

| Command | Use when |
|---------|----------|
| `rmdir` | Directory is empty and you want a safe delete |
| `rm -r` | Directory has files inside it |
| `rm -rf` | Force delete everything — use only when certain |

---

## Key Concepts from Day 02

| Concept | Key point |
|---------|-----------|
| Hidden files | Start with `.` — only visible with `ls -a` |
| `-r` flag | Required for any command acting on a directory recursively |
| `mv` vs `cp` | `cp` keeps the original. `mv` does not. |
| `rm` is permanent | No undo. No recycle bin. Always double-check. |
| `mkdir -p` | Creates nested folders in one command |



---

*Next: File permissions (chmod, chown), viewing file contents (cat, less, head, tail), and the man command*