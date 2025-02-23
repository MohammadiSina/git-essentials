## 4. Undoing Changes and Fixes

Sometimes, mistakes happen. Git provides multiple ways to undo changes at various stages of your workflow. This section covers three primary methods: reverting commits, resetting commits, and restoring changes in your working directory.

---

### Reverting a Commit

**Command:**
```bash
git revert <commit-hash>
```
**What it does:** Creates a new commit that undoes the changes introduced by the specified commit. This method preserves the commit history and is safe for shared branches.

**Example:**
```bash
git log --oneline
# Suppose the commit you want to revert is ab12cd3
git revert ab12cd3
```
This creates a new commit that reverses the changes from `ab12cd3`.

**Exercise:**
1. Identify a recent commit using `git log --oneline`.
2. Revert that commit using `git revert <commit-hash>`.
3. Run `git log --oneline` to see the new revert commit in your history.

---

### Resetting Commits

`git reset` moves the branch pointer to a previous commit and can modify your staging area and working directory based on the chosen option.

#### Soft Reset

**Command:**
```bash
git reset --soft HEAD~1
```
**What it does:** Moves the HEAD pointer back one commit but leaves your changes staged.

**Example:**
```bash
git commit -m "Temporary commit"
git reset --soft HEAD~1
```
After this, your changes remain staged, allowing you to recommit them if needed.

#### Mixed Reset (Default)

**Command:**
```bash
git reset HEAD~1
```
or
```bash
git reset --mixed HEAD~1
```
**What it does:** Moves the HEAD pointer back one commit and unstages the changes, but leaves the modifications in your working directory.

#### Hard Reset

**Command:**
```bash
git reset --hard HEAD~1
```
**What it does:** Moves the HEAD pointer back one commit and discards all changes in the staging area and working directory. **Warning:** This command will permanently delete uncommitted changes.

**Exercise:**
1. Make a commit (e.g., `git commit -m "Test commit"`).
2. Use `git reset --soft HEAD~1` and check the status to see your changes still staged.
3. Repeat with `--mixed` and observe that changes are unstaged but remain in the working directory.
4. **(Optional and careful!)** Try `--hard` in a test branch to see how it discards changes.

---

### Restoring Changes in the Working Directory

Sometimes you only want to undo changes in your working directory without altering commit history.

#### Using git restore

**Command for unstaged changes:**
```bash
git restore <file>
```
**What it does:** Reverts the changes in the specified file back to the last committed state.

**Example:**
```bash
echo "Temporary changes" >> example.txt
git status
git restore example.txt
```
After running, `example.txt` reverts to its previous state.

**Command for staged changes:**
```bash
git restore --staged <file>
```
**What it does:** Removes the file from the staging area while keeping the changes in the working directory.

**Exercise:**
1. Modify a file and check its status.
2. Stage the changes using `git add`.
3. Run `git restore --staged <file>` to unstage it.
4. Run `git status` to confirm that the file is no longer staged.
5. Then, use `git restore <file>` to discard the changes completely.

---

These commands give you the flexibility to undo mistakes at various stages—whether you want to preserve history or simply clear uncommitted changes. Practice each method to understand how they affect your repository.
