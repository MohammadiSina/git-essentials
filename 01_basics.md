##  1. Git Basics

###  Initializing a Repository

**Command:**
```bash
git init
```
**What it does:** Initializes a new Git repository in your current directory.

**Example:**
```bash
mkdir my-project
cd my-project
git init
```
This creates a `.git` folder, allowing Git to track your project. The folder is hidden by default.

---

###  Checking Status

**Command:**
```bash
git status
```
**What it does:** Shows the state of the working directory and staging area.

**Example Output:**
```
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
```
---

###  Staging Changes

**Command:**
```bash
git add .
```
**What it does:** Stages all changes in the current directory, except file deletions.

**Command:**
```bash
git add -A
```
**What it does:** Stages all changes, including deletions.

**Exercise:**
1. Create a new file (`hello.txt`).
2. Run `git add .` and check status.
3. Delete the file and try `git add -A`.
4. Check the status again.

---

###  Committing Changes

**Command:**
```bash
git commit -m "Initial commit"
```
**What it does:** Records changes with a short message.

**Alternative:**
```bash
git commit
```
Without `-m`, Git opens an editor for a detailed commit message.

**Exercise:**
1. Make some edits to a file.
2. Stage the changes.
3. Commit with and without using `-m`.

---
### Viewing Commit History

**Command:**
```bash
git log --oneline
```
**What it does:** Shows a simplified, one-line-per-commit log. Another useful flag for this command is `--graph` which tries to show the commits and branches using a pattern.

**Example Output:**
```
ab12cd3 Initial commit
9f8e7d6 Added README
```

**Exercise:**
1. Run `git log --oneline` and observe the commit history.
2. Add a new commit and see how the log updates.

