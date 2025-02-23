## 2. Branching and Merging

### Creating and Switching Branches

**Command:**
```bash
git checkout -b feature-login
```
**What it does:** Creates a new branch named `feature-login` and switches to it immediately.

**Exercise:**
1. In your repository, create a new branch called `feature-update`.
2. Verify that you are on `feature-update` by running:
   ```bash
   git branch
   ```
---

### Merging Branches
**Command to switch to the target branch:**
```bash
git checkout master
```
Or

```bash
git switch master
```
**What it does:** Switches to the `master` branch (or your main branch).

**Command to merge:**
```bash
git merge feature-login
```
**What it does:** Merges the changes from the `feature-login` branch into the current branch (which should be `master`).

**Example:**
```bash
git checkout master
git merge feature-login
```
This integrates the changes from the feature branch into the master branch. Note that before merging, you must switch your branch to your primary one.

**Exercise:**
1. Create a branch `feature-test` and make at least one commit.
2. Switch to `master` and merge `feature-test`.
3. Verify the merge by running:
   ```bash
   git log --oneline --graph
   ```

---

### Rebasing Branches

**Command to rebase:**
```bash
git checkout feature-update
git rebase master
```
**What it does:** Moves the commits in `feature-update` so they appear on top of the latest commit in `master`, resulting in a linear and cleaner history.

**Example:**
```bash
git checkout feature-update
git rebase master
```
If conflicts occur during the rebase, resolve them manually, then stage the resolved files:
```bash
git add <file>
git rebase --continue
```

**Exercise:**
1. Create a branch `rebase-demo` and make a couple of commits.
2. Switch to `master` and make a commit.
3. Switch back to `rebase-demo` and rebase it onto `master`.
4. Verify the linear history with:
   ```bash
   git log --oneline --graph
   ```

---

### Deleting Branches

**Command:**
```bash
git branch -d feature-login
```
**What it does:** Deletes the branch `feature-login` if it has been merged into the current branch. If you want to delete a branch that hasn't been merged or whatever, use the `-D` flag.


**Exercise:**
1. After merging a branch, delete it using the above command.
2. Check if it has been done.
