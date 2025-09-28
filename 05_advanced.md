# 5. Advanced Git Techniques

Advanced Git tools help you handle complex workflows and troubleshooting. This section covers Git Stash, Cherry-Pick, Bisect, Worktree, and other modern Git features.

---

## Git Stash

**What it does:** Temporarily saves changes that are not ready to be committed, allowing you to switch branches or work on something else without losing your progress.

### Basic Stash Commands

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

### Modern Stash Features

- **Stash with a message:**
  ```bash
  git stash push -m "Work in progress on feature X"
  ```
  **What it does:** Creates a stash with a descriptive message for better organization.

- **Stash specific files:**
  ```bash
  git stash push -m "Partial work" -- file1.txt file2.txt
  ```
  **What it does:** Stashes only specific files instead of all changes.

- **Stash including untracked files:**
  ```bash
  git stash -u
  ```
  **What it does:** Includes untracked files in the stash.

- **Export stashes:**
  ```bash
  git stash create
  ```
  **What it does:** Creates a stash that can be exported as a reference, allowing you to push/pull stashes like branches.

**Exercise:**
1. Make some changes in your repository (modify or create a file).
2. Run `git stash push -m "Test stash"` to save these changes with a message.
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

---

## Git Worktree

**What it does:** Allows you to have multiple working directories associated with a single Git repository, enabling you to work on different branches simultaneously without switching between them.

### Basic Worktree Commands

- **Create a new worktree:**
  ```bash
  git worktree add ../feature-branch feature-branch
  ```
  **What it does:** Creates a new working directory for the `feature-branch` in the parent directory.

- **List all worktrees:**
  ```bash
  git worktree list
  ```
  **What it does:** Shows all worktrees associated with the repository.

- **Remove a worktree:**
  ```bash
  git worktree remove ../feature-branch
  ```
  **What it does:** Removes the specified worktree (the directory must be clean).

- **Prune worktrees:**
  ```bash
  git worktree prune
  ```
  **What it does:** Removes references to worktrees that no longer exist.

### Advanced Worktree Features

- **Create worktree from a specific commit:**
  ```bash
  git worktree add ../hotfix-branch abc1234
  ```
  **What it does:** Creates a worktree from a specific commit hash.

- **Lock a worktree:**
  ```bash
  git worktree lock ../feature-branch
  ```
  **What it does:** Prevents the worktree from being removed accidentally.

**Exercise:**
1. Create a new branch and a worktree for it.
2. Make changes in both the main directory and the worktree.
3. Switch between them to see how they work independently.

---

## Git Submodules

**What it does:** Allows you to include one Git repository as a subdirectory of another Git repository, keeping the repositories separate but linked.

### Basic Submodule Commands

- **Add a submodule:**
  ```bash
  git submodule add https://github.com/user/repo.git path/to/submodule
  ```
  **What it does:** Adds a repository as a submodule at the specified path.

- **Initialize submodules:**
  ```bash
  git submodule init
  ```
  **What it does:** Initializes the submodules defined in `.gitmodules`.

- **Update submodules:**
  ```bash
  git submodule update
  ```
  **What it does:** Updates submodules to the commit specified by the parent repository.

- **Clone with submodules:**
  ```bash
  git clone --recurse-submodules <repo-url>
  ```
  **What it does:** Clones a repository and all its submodules in one command.

---

## Performance and Maintenance

### Git Maintenance

- **Run maintenance tasks:**
  ```bash
  git maintenance run
  ```
  **What it does:** Runs various maintenance tasks to optimize repository performance.

- **Enable automatic maintenance:**
  ```bash
  git maintenance start
  ```
  **What it does:** Enables automatic background maintenance tasks.

- **Repack with optimizations:**
  ```bash
  git repack -ad --cruft
  ```
  **What it does:** Repacks the repository with cruft pack optimization for better performance.

### Git Config Optimizations

- **Enable multi-pack index:**
  ```bash
  git config core.multiPackIndex true
  ```
  **What it does:** Enables multi-pack index for faster repository access.

- **Set commit graph:**
  ```bash
  git config core.commitGraph true
  ```
  **What it does:** Enables commit graph for faster commit history queries.

---

These advanced tools provide powerful ways to manage your workflow, debug issues, and optimize your Git repository performance. Practice each command to understand its impact on your repository.
