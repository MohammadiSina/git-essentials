## 5. Advanced Git Techniques

Advanced Git tools help you handle complex workflows and troubleshooting. This section covers Git Stash, Cherry-Pick, and Bisect.

---

### Git Stash

**What it does:** Temporarily saves changes that are not ready to be committed, allowing you to switch branches or work on something else without losing your progress.

**Commands:**

- **Stash changes:**
  ```bash
  git stash
  ```
  This command saves your uncommitted changes and reverts your working directory to the last commit.

- **List stashes:**
  ```bash
  git stash list
  ```
  Displays a list of all stashed changes.

- **Apply the latest stash (without removing it):**
  ```bash
  git stash apply
  ```

- **Apply and remove the latest stash:**
  ```bash
  git stash pop
  ```

- **Clear all stashes:**
  ```bash
  git stash clear
  ```

**Exercise:**
1. Make some changes in your repository (modify or create a file).
2. Run `git stash` to save these changes.
3. Verify the stash with `git stash list`.
4. Use `git stash pop` to reapply the changes and remove them from the stash list.
5. Confirm your changes are back in your working directory.

---

### Git Cherry-Pick

**What it does:** Applies a specific commit from one branch onto your current branch, without merging the entire branch history.

**Command:**
```bash
git cherry-pick <commit-hash>
```
**Example:**
1. Check the commit history:
   ```bash
   git log --oneline
   ```
2. Copy the hash of the commit you want to apply (e.g., `abc1234`).
3. On your current branch, run:
   ```bash
   git cherry-pick abc1234
   ```
   This creates a new commit with the changes from `abc1234`.

**Exercise:**
1. Create a new branch and make a commit.
2. Switch to another branch.
3. Use `git cherry-pick` with the commit hash from the first branch.
4. Verify that the commit has been applied by checking the commit history.

---

### Git Bisect

**What it does:** Helps you identify the commit that introduced a bug by using a binary search through your commit history.

**Workflow:**

1. **Start bisecting:**
   ```bash
   git bisect start
   ```
2. **Mark the current commit as bad:**
   ```bash
   git bisect bad
   ```
3. **Mark a known good commit:**
   ```bash
   git bisect good <good-commit-hash>
   ```
4. Git will automatically check out a commit halfway between the good and bad commits. Test this commit:
   - If the bug is present, mark it as bad:
     ```bash
     git bisect bad
     ```
   - If the bug is not present, mark it as good:
     ```bash
     git bisect good
     ```
5. Repeat the process until Git identifies the commit that introduced the bug.

6. **Finish bisecting:**
   ```bash
   git bisect reset
   ```

**Exercise:**
1. Introduce a small, deliberate bug in one commit.
2. Use `git bisect` to navigate through your commit history.
3. Mark commits as good or bad based on the presence of the bug.
4. Confirm that Git pinpoints the problematic commit.
5. Reset bisect mode after finishing.

---

These advanced tools provide powerful ways to manage your workflow and debug issues. Practice each command to understand its impact on your repository.
