# Git Basics — Day 02 Notes
**Date:** 2026-03-19  
**Source:** [Pro Git Book — Chapter 2](https://git-scm.com/book/en/v2)  
**Topic:** Viewing history, undoing changes, working with remotes

---

## git log — View Commit History
Shows the full history of commits in the current repository, most recent first.

```bash
git log                          # full log — hash, author, date, message
git log --pretty=oneline         # compact — one commit per line
git log --oneline                # even shorter shorthand (same effect)
git log --oneline --graph        # visual branch graph in the terminal
git log -5                       # show only the last 5 commits
```

Example output of `git log --pretty=oneline`:
```
a3f9c21 Day 2: Git log, amend, reset, restore and remotes
b1d8e44 Day 1: Linux basics and Git chapter 2 staging notes
```

> The long string of letters and numbers is the **commit hash** — Git's unique ID for that commit. You use it to reference specific commits.

---

## git commit --amend — Fix Your Last Commit
Lets you modify the most recent commit — either to fix the message or to add files you forgot to include.

```bash
# Fix a typo in your last commit message
git commit --amend -m "Day 2: Git log, amend, reset, restore and remotes"

# Add a forgotten file to the last commit
git add forgotten-file.md
git commit --amend --no-edit      # --no-edit keeps the existing message
```

> ⚠️ Only amend commits that have NOT been pushed to GitHub yet. Amending a pushed commit rewrites history and causes problems for others.

---

## git reset HEAD — Unstage a File
Removes a file from the staging area and puts it back to modified (unstaged). Your actual file changes are kept — nothing is deleted.

```bash
git reset HEAD notes.txt         # unstage notes.txt — keeps your changes
git reset HEAD                   # unstage everything currently staged
```

> Think of this as the undo button for `git add`. You staged something by mistake — this takes it back out.

**What changes and what doesn't:**

| | Before reset | After reset |
|--|-------------|-------------|
| File content | Changed | Still changed ✅ |
| Staging area | File is staged | File is unstaged |
| Commit history | Unchanged | Unchanged |

---

## git restore — Discard Changes in Working Directory
Throws away unsaved changes in a file and restores it to the last committed version.

```bash
git restore notes.txt            # discard all changes to notes.txt
git restore .                    # discard all changes in the whole repo
git restore --staged notes.txt   # unstage a file (same effect as git reset HEAD)
```

> ⚠️ This is destructive — your unsaved changes are gone permanently. Use with care.

**git reset vs git restore — what's the difference?**

| Command | What it does | Destructive? |
|---------|-------------|--------------|
| `git reset HEAD file` | Unstages the file, keeps your changes | ❌ No |
| `git restore file` | Discards your changes entirely | ✅ Yes |
| `git restore --staged file` | Unstages the file (same as reset HEAD) | ❌ No |

---

## git remote -v — View Remote Connections
Shows the remote repositories your local repo is connected to, and their URLs.

```bash
git remote -v
```

Example output:
```
origin  https://github.com/OladapoOG/linux-learning-notes.git (fetch)
origin  https://github.com/OladapoOG/linux-learning-notes.git (push)
```

> `origin` is the default name Git gives to the remote you cloned from. `fetch` = where you pull from. `push` = where you send commits to. Usually both point to the same URL.

---

## git remote add — Connect to a Remote Repository
Links your local repository to a remote one on GitHub (or elsewhere).

```bash
git remote add origin https://github.com/OladapoOG/linux-learning-notes.git
```

> You only need this when you created a repo locally with `git init` and want to connect it to GitHub. If you used `git clone`, the remote is already set up automatically.

**Common remote commands:**

```bash
git remote -v                              # view all remotes
git remote add origin <url>               # add a new remote called origin
git remote set-url origin <new-url>       # change the URL of an existing remote
git remote remove origin                  # disconnect from a remote
```

---

## The Undo Cheat Sheet

| Situation | Command |
|-----------|---------|
| Fix the last commit message | `git commit --amend -m "new message"` |
| Add a forgotten file to last commit | `git add file` then `git commit --amend --no-edit` |
| Unstage a file (keep changes) | `git reset HEAD filename` or `git restore --staged filename` |
| Discard all changes to a file | `git restore filename` |
| See what remotes you're connected to | `git remote -v` |

---

## Key Takeaways from Day 02 Git

- `git log --oneline` is the fastest way to scan your commit history
- `git commit --amend` is a lifesaver for fixing small mistakes — but only before pushing
- `git reset HEAD` and `git restore --staged` both unstage files — neither deletes your work
- `git restore` (without `--staged`) **does** delete your work — use carefully
- `origin` is just a name — it points to your GitHub repo URL

---

*Next: Git Branching — Chapter 3 (creating branches, switching, merging, resolving conflicts)*