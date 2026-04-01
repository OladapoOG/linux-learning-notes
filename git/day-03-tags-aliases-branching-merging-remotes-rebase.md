# Git — Chapters 2 & 3 Completion Notes
**Date:** 2026-03-21  
**Source:** [Pro Git Book — Chapters 2 & 3](https://git-scm.com/book/en/v2)  
**Topics:** Tagging, Aliases, Branching, Merging, Remote Branches, Tracking Branches, Rebasing

---

## git tag — Mark Important Points in History
Tags are used to mark specific commits as significant — most commonly used to mark release versions.

```bash
git tag                              # list all existing tags
git tag v1.0                         # create a lightweight tag on current commit
git tag -a v1.4 -m "my version 1.4"  # create an annotated tag with a message
git tag -a v1.2 9fceb02              # tag a specific past commit using its hash
git push origin v1.4                 # push a specific tag to GitHub
git push origin --tags               # push all tags to GitHub
```

**Lightweight vs Annotated tags:**

| Type | Command | Use for |
|------|---------|---------|
| Lightweight | `git tag v1.0` | Quick personal bookmarks |
| Annotated | `git tag -a v1.0 -m "message"` | Official releases — stores author, date, message |

> Tags are not pushed automatically with `git push`. You must push them explicitly.

---

## git config alias — Create Shortcuts for Commands
Aliases let you type shorter versions of long commands. Saves time and reduces typos.

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```

After setting these up:
```bash
git co main          # same as: git checkout main
git br               # same as: git branch
git ci -m "message"  # same as: git commit -m "message"
git st               # same as: git status
```

> You can create aliases for any command — including long ones you use often.
> Example: `git config --global alias.last 'log -1 HEAD'` → `git last` shows your last commit.

---

## Git Branching — The Core Concept
A branch is simply a pointer to a specific commit. Creating a branch is instant and lightweight in Git — it does not copy your files.

**Why branching matters in DevOps:**
You never work directly on the main branch in a professional environment. Every feature, fix, or infrastructure change gets its own branch, reviewed, then merged in. This protects the main codebase.

---

## Creating and Switching Branches

```bash
git branch testing               # create a new branch called testing
git checkout testing             # switch to the testing branch (older syntax)
git checkout -b newbranchname    # create AND switch to a new branch in one command

# Modern syntax (Git 2.23+)
git switch testing               # switch to testing branch
git switch -c new-branch         # create AND switch to new branch
git switch -                     # switch back to the previous branch
```

> `git switch` is the newer, cleaner way to change branches. `git checkout` still works but does too many things — switch was introduced to be more explicit.

---

## git log --oneline --decorate
Shows commit history with branch and tag pointers clearly labelled.

```bash
git log --oneline --decorate
git log --oneline --decorate --graph --all   # full visual of all branches
```

Example output:
```
f30ab (HEAD -> main, origin/main) Day 3: Git branching notes
34ac2 Day 2: Linux files and directories
98ca9 Day 1: Initial commit
```

> `HEAD` tells you which branch you are currently on. `HEAD -> main` means you are on the main branch.

---

## git commit -a -m — Stage and Commit in One Step
Automatically stages all **tracked** modified files and commits them in one command.

```bash
git commit -a -m "Day 3: Add branching notes"
```

> ⚠️ This only works for files Git is already tracking. Brand new files (untracked) still need `git add` first.

---

## Basic Merging
Merging brings the changes from one branch into another.

```bash
git checkout main          # switch to the branch you want to merge INTO
git merge testing          # merge the testing branch into main
```

**Two types of merge:**

| Type | When it happens | What it does |
|------|----------------|--------------|
| Fast-forward | No new commits on main since branching | Simply moves the pointer forward — no merge commit |
| 3-way merge | Both branches have new commits | Creates a new merge commit combining both histories |

```bash
git mergetool              # opens a visual tool to resolve merge conflicts
```

> Merge conflicts happen when two branches changed the same part of the same file. Git can't decide which version to keep — you resolve it manually.

---

## Branch Management

```bash
git branch                          # list all local branches (* = current branch)
git branch -v                       # list branches with their latest commit message
git branch --merged                 # branches already merged into current branch (safe to delete)
git branch --no-merged              # branches NOT yet merged (deletion will be blocked)
git branch -d branchname            # delete a merged branch safely
git branch -D branchname            # force delete an unmerged branch

# Renaming a branch
git branch --move bad-branch-name corrected-branch-name   # rename locally
git push origin corrected-branch-name                     # push the renamed branch
git push origin --delete bad-branch-name                  # delete the old name on GitHub
```

> Always check `git branch --merged` before deleting branches — if it shows up there, it is safe to delete.

---

## Remote Branches
Remote branches are pointers to the state of branches on your remote repository (GitHub). They are named `remote/branch` e.g. `origin/main`.

```bash
git fetch origin                    # download all updates from GitHub without merging
git fetch <remote>                  # fetch from a specific remote

git push origin main                # push local main branch to GitHub
git push <remote> <branch>          # push any branch to any remote
git push origin --delete branchname # delete a branch on GitHub
```

> `git fetch` updates your remote tracking branches (e.g. `origin/main`) but does NOT change your local `main`. You stay in control of when to merge.

---

## Tracking Branches
A tracking branch is a local branch that has a direct relationship with a remote branch. When you clone a repo, `main` automatically tracks `origin/main`.

```bash
git checkout -b mybranch origin/mybranch    # create a local branch that tracks a remote branch
git checkout --track origin/mybranch        # shorthand for the same thing

git pull                                    # fetch + merge tracked remote branch into current branch
```

> When a local branch tracks a remote, `git pull` knows exactly where to pull from without you specifying.

---

## Rebasing
Rebase takes your commits and replays them on top of another branch, creating a clean linear history.

```bash
git checkout mybranch
git rebase main              # replay mybranch commits on top of main

git rebase --abort           # cancel a rebase in progress
git rebase --continue        # continue after resolving a conflict mid-rebase
```

**Rebase vs Merge:**

| | Merge | Rebase |
|--|-------|--------|
| History | Preserves full branching history | Creates a clean straight line |
| Merge commit | Yes | No |
| Rewrites history | No | Yes |
| Best for | Team shared branches | Cleaning up local work before sharing |

**The golden rule — never forget this:**
> ⚠️ Do not rebase commits that exist outside your local repository and that others may have based work on. Rebase rewrites history — doing it on shared/pushed branches causes serious problems for teammates.

**Safe:** Rebase your own local feature branch before merging into main.  
**Never:** Rebase main, or any branch others are working from.

---

## Chapters 2 & 3 Complete ✅

### Full command reference — everything covered so far

```bash
# Setup
git config --global user.name "Name"
git config --global user.email "email"
git config --global alias.st status

# Basics
git clone <url>
git status
git add .
git commit -m "message"
git commit -a -m "message"
git push
git pull

# History & undoing
git log --oneline --decorate --graph
git commit --amend -m "fixed message"
git reset HEAD filename
git restore filename
git restore --staged filename

# Tags
git tag -a v1.0 -m "version 1.0"
git push origin --tags

# Branching
git branch branchname
git switch -c branchname
git switch main
git merge branchname
git branch --merged
git branch -d branchname

# Remotes
git remote -v
git remote add origin <url>
git fetch origin
git push origin branchname
git push origin --delete branchname

# Rebasing
git rebase main
```

---