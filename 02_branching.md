# 2. Branching and Merging

## Creating and Switching Branches

**Traditional Command:**
```bash
git checkout -b feature-login
```
**What it does:** Creates a new branch named `feature-login` and switches to it immediately.

**Modern Command:**
```bash
git switch -c feature-login
```
**What it does:** Same as above but uses the dedicated `git switch` command, which is more intuitive and less ambiguous than `git checkout`.

**Switching to Existing Branches:**
```bash
git switch feature-login
```
**What it does:** Switches to an existing branch (modern alternative to `git checkout branch-name`).

**Exercise:**
1. In your repository, create a new branch called `feature-update` using `git switch -c`.
2. Verify that you are on `feature-update` by running:
   ```bash
   git branch
   ```

---

## Merging Branches

**Command to switch to the target branch:**
```bash
git switch main
```
**What it does:** Switches to the `main` branch (modern default branch name).

**Command to merge:**
```bash
git merge feature-login
```
**What it does:** Merges the changes from the `feature-login` branch into the current branch (which should be `main`).

**Example:**
```bash
git switch main
git merge feature-login
```
This integrates the changes from the feature branch into the main branch. Note that before merging, you must switch your branch to your primary one.

**Modern Merge Strategies:**
- **Fast-forward merge:** `git merge --ff-only feature-login` (only if no divergence)
- **No fast-forward:** `git merge --no-ff feature-login` (always creates merge commit)
- **Squash merge:** `git merge --squash feature-login` (combines all commits into one)

**Exercise:**
1. Create a branch `feature-test` and make at least one commit.
2. Switch to `main` and merge `feature-test`.
3. Verify the merge by running:
   ```bash
   git log --oneline --graph
   ```

---

## Rebasing Branches

**Command to rebase:**
```bash
git switch feature-update
git rebase main
```
**What it does:** Moves the commits in `feature-update` so they appear on top of the latest commit in `main`, resulting in a linear and cleaner history.

**Example:**
```bash
git switch feature-update
git rebase main
```
If conflicts occur during the rebase, resolve them manually, then stage the resolved files:
```bash
git add <file>
git rebase --continue
```

**Interactive Rebasing:**
```bash
git rebase -i HEAD~3
```
**What it does:** Allows you to edit, reorder, or squash commits interactively.

**Exercise:**
1. Create a branch `rebase-demo` and make a couple of commits.
2. Switch to `main` and make a commit.
3. Switch back to `rebase-demo` and rebase it onto `main`.
4. Verify the linear history with:
   ```bash
   git log --oneline --graph
   ```

---

## Deleting Branches

**Command:**
```bash
git branch -d feature-login
```
**What it does:** Deletes the branch `feature-login` if it has been merged into the current branch.

**Force Delete:**
```bash
git branch -D feature-login
```
**What it does:** Force deletes the branch even if it hasn't been merged (use with caution).

**Delete Remote Branch:**
```bash
git push origin --delete feature-login
```
**What it does:** Deletes the branch on the remote repository.

**Exercise:**
1. After merging a branch, delete it using the above command.
2. Check if it has been done.
