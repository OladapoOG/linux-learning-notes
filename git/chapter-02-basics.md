# Git Basics — Chapter 2 Notes
**Date:** 2026-03-18  
**Source:** [Pro Git Book — Chapter 2](https://git-scm.com/book/en/v2)  
**Topic:** Git basics — staging, tracking, and working with a repository

---

## What is a Git Repository?
A Git repository is a folder that Git is tracking. It stores the full history of every change ever made to the files inside it. There are two ways to get one:

1. Initialise a new one yourself with `git init`
2. Copy an existing one from somewhere like GitHub with `git clone`

---

## git clone — Copy a Remote Repository
Downloads a complete copy of a remote repository to your local machine, including all history.

```bash
git clone https://github.com/username/repository-name.git
# Creates a folder called repository-name with everything inside it

git clone https://github.com/username/repository-name.git my-folder
# Same but saves it into a folder called my-folder instead
```

> This is how you get a repo from GitHub onto your computer. You only do this once per project.

---

## git config — Set Your Identity
Before you can commit anything, Git needs to know who you are. These settings are saved globally so you only set them once.

```bash
git config --global user.name "Oladapo Ogunfeitimi"
git config --global user.email "dapoogunfeitimi950@gmail.com"
```

> `--global` means this applies to every Git repo on your machine. Without your name and email, Git won't let you commit.

Verify your config at any time:
```bash
git config --list
```

---

## The Three States — Most Important Concept in Git

Every file in a Git repo lives in one of three states:

```
Working Directory  →  Staging Area  →  Git Repository
  (you edit here)     (you prepare     (committed,
                        here)           saved forever)
```

| State | What it means |
|-------|---------------|
| **Modified** | You changed the file but haven't told Git yet |
| **Staged** | You've marked the file to go into the next commit |
| **Committed** | The change is permanently saved in Git history |

> Think of staging like packing a box before shipping. You decide exactly what goes in before you seal it (commit).

---

## git status — Check What's Going On
Shows which files are modified, staged, or untracked. Run this constantly — it's your compass.

```bash
git status
```

Example output:
```
On branch main
Changes to be committed:           ← STAGED (ready to commit)
  modified: README.md

Changes not staged for commit:     ← MODIFIED but NOT staged yet
  modified: notes.txt

Untracked files:                   ← Git doesn't know about these yet
  new-file.txt
```

> If you're ever unsure what state your repo is in, `git status` is the first command to run.

---

## git add — Stage Your Changes
Moves changes from the working directory into the staging area.

```bash
git add filename.txt        # stage a single file
git add .                   # stage ALL changed files in the current directory
git add linux/              # stage all files inside the linux/ folder
```

> `git add .` is the most common. It stages everything you've changed. Be careful — make sure you actually want to commit everything first.

---

## git diff — See Exactly What Changed
Shows the line-by-line differences between your working directory and the staging area.

```bash
git diff                    # shows changes NOT yet staged
git diff --staged           # shows changes that ARE staged (ready to commit)
```

> Lines starting with `+` are additions. Lines starting with `-` are deletions. This is how you review your work before committing.

---

## The Difference Between Staged and Unstaged

| | Unstaged | Staged |
|--|---------|--------|
| **What it is** | Changes you've made but not added yet | Changes you've run `git add` on |
| **Shows in** | `git diff` | `git diff --staged` |
| **Will it be committed?** | ❌ No | ✅ Yes |
| **How to move it** | Run `git add filename` | Already ready |

**Why this matters in DevOps:** You might change 5 files but only want to commit 2 of them right now. Staging lets you be precise about what goes into each commit. Clean, logical commits make debugging and collaboration much easier.

---

## git commit — Save Your Staged Changes
Permanently records everything in the staging area into the repository history.

```bash
git commit -m "Day 1: Add Linux basic commands notes"
```

> Always write a clear, descriptive commit message. Future you (and teammates) will thank you.  
> Bad message: `git commit -m "update"`  
> Good message: `git commit -m "Day 1: Linux - pwd, cd, whoami, cp, rm, echo"`

---

## git push — Send Commits to GitHub
Uploads your local commits to the remote repository on GitHub.

```bash
git push                        # push to the default remote and branch
git push origin main            # explicitly push to the main branch on origin
```

> `origin` is the name Git gives to the remote repository you cloned from (GitHub). `main` is the branch name.

---

## Daily Commit Workflow — Your Routine

```bash
# 1. Make changes to your notes files
# 2. Check what you've changed
git status

# 3. Review the actual changes
git diff

# 4. Stage your files
git add .

# 5. Commit with a clear message
git commit -m "Day 2: Git - staging area, git add, git diff"

# 6. Push to GitHub
git push
```

> Do this every single day. It builds your GitHub activity graph and reinforces your learning.

---

## Key Takeaways from Chapter 2

- Git tracks **changes**, not whole files
- The **staging area** is what makes Git powerful — you control exactly what goes into each commit
- `git status` is your best friend — run it constantly
- A good commit message describes **what** you changed and **why**
- `git add .` → `git commit -m "message"` → `git push` is the core loop you will repeat thousands of times

---

*Next: Chapter 3 — Git Branching (creating branches, merging, resolving conflicts)*