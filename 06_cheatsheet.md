# 6. Git Cheat Sheet

## Git Basics
- **git init**  
  Initialize a new Git repository.

- **git init --object-format=sha256**  
  Initialize a new Git repository with SHA-256 (modern standard).

- **git status**  
  Display the state of the working directory and staging area.

- **git status --porcelain**  
  Display status in machine-readable format.

- **git add .**  
  Stage all new and modified files (excluding deletions).

- **git add -A** / **git add --all**  
  Stage all changes, including deletions.

- **git commit -m "message"**  
  Commit staged changes with a short message.

- **git commit**  
  Open the default editor to write a detailed commit message.

- **git log --oneline**  
  Show commit history in a one-line format.

- **git log --oneline --graph --decorate --all**  
  Display comprehensive commit history with all branches.

---

## Branching and Merging
- **git branch**  
  List all local branches.

- **git switch -c branch-name**  
  Create a new branch and switch to it (modern command).

- **git checkout -b branch-name**  
  Create a new branch and switch to it (legacy command).

- **git switch branch-name**  
  Switch to an existing branch (modern command).

- **git checkout branch-name**  
  Switch to an existing branch (legacy command).

- **git merge branch-name**  
  Merge the specified branch into the current branch.

- **git merge --no-ff branch-name**  
  Merge with no fast-forward (always creates merge commit).

- **git merge --squash branch-name**  
  Squash merge (combines all commits into one).

- **git rebase branch-name**  
  Rebase the current branch onto the specified branch for a linear history.

- **git rebase -i HEAD~3**  
  Interactive rebase for the last 3 commits.

- **git branch -d branch-name**  
  Delete the specified branch (only if it has been merged).

- **git branch -D branch-name**  
  Force delete the specified branch.

- **git push origin --delete branch-name**  
  Delete the branch on the remote repository.

---

## Remote Repositories
- **git remote add origin <repo-url>**  
  Add a remote repository and name it `origin`.

- **git remote -v**  
  List all remote repositories and their URLs.

- **git push -u origin branch-name**  
  Push the branch to `origin` and set it as the default upstream branch.

- **git push origin main**  
  Push the main branch to origin.

- **git pull**  
  Fetch and merge changes from the remote repository.

- **git pull --rebase**  
  Fetch and rebase changes from the remote repository.

- **git fetch**  
  Fetch new commits from the remote without merging.

- **git fetch --all**  
  Fetch from all remotes.

- **git clone <repo-url>**  
  Clone a remote repository to your local machine.

- **git clone --recurse-submodules <repo-url>**  
  Clone a repository with all its submodules.

---

## Undoing Changes
- **git revert <commit-hash>**  
  Create a new commit that undoes the changes of a specified commit.

- **git revert <commit1> <commit2>**  
  Revert multiple commits in sequence.

- **git revert <oldest>..<newest>**  
  Revert a range of commits.

- **git reset --soft HEAD~1**  
  Move HEAD to the previous commit, keeping changes staged.

- **git reset --mixed HEAD~1**  
  Reset to the previous commit and unstage changes (default mode).

- **git reset --hard HEAD~1**  
  Reset to the previous commit and discard all changes (use with caution).

- **git restore <file>**  
  Revert changes in a file back to the last committed state (modern command).

- **git restore --staged <file>**  
  Unstage a file while keeping its modifications in the working directory.

- **git restore --source=HEAD~2 <file>**  
  Restore a file to the state it was in two commits ago.

- **git restore .**  
  Restore all modified files in the current directory.

- **git restore --staged .**  
  Unstage all staged files in the current directory.

- **git checkout -- <file>**  
  Revert changes in a file (legacy command).

- **git reset HEAD <file>**  
  Unstage a file (legacy command).

---

## Advanced Git
- **git stash**  
  Temporarily save uncommitted changes.

- **git stash push -m "message"**  
  Save changes with a descriptive message.

- **git stash push -- file1 file2**  
  Stash only specific files.

- **git stash -u**  
  Stash including untracked files.

- **git stash list**  
  List all saved stashes.

- **git stash apply**  
  Reapply the latest stash without removing it from the stash list.

- **git stash pop**  
  Reapply the latest stash and remove it from the stash list.

- **git stash clear**  
  Remove all stashes.

- **git cherry-pick <commit-hash>**  
  Apply a specific commit from another branch onto the current branch.

- **git bisect start**  
  Begin a binary search to find the commit that introduced a bug.

- **git bisect bad/good**  
  Mark commits as bad or good during the bisect process.

- **git bisect reset**  
  End the bisect session and return to the original branch.

## Git Worktree
- **git worktree add <path> <branch>**  
  Create a new worktree for a branch.

- **git worktree list**  
  List all worktrees.

- **git worktree remove <path>**  
  Remove a worktree.

- **git worktree prune**  
  Remove references to deleted worktrees.

## Git Submodules
- **git submodule add <url> <path>**  
  Add a submodule to the repository.

- **git submodule init**  
  Initialize submodules.

- **git submodule update**  
  Update submodules to the specified commit.

- **git submodule status**  
  Show the status of submodules.

## Performance and Maintenance
- **git maintenance run**  
  Run repository maintenance tasks.

- **git maintenance start**  
  Enable automatic maintenance.

- **git repack -ad --cruft**  
  Repack repository with cruft optimization.

- **git fsck --full**  
  Check repository integrity.

---

## Configuration Commands
- **git config --global user.name "Your Name"**  
  Set your global Git username.

- **git config --global user.email "youremail@example.com"**  
  Set your global Git email.

- **git config --global init.defaultBranch main**  
  Set the default branch name to 'main'.

- **git config --global core.autocrlf false**  
  Disable automatic line ending conversion.

- **git config --global core.multiPackIndex true**  
  Enable multi-pack index for better performance.

- **git config --global core.commitGraph true**  
  Enable commit graph for faster history queries.

## Comparison Commands
- **git diff**  
  Display differences between commits, branches, or the working directory.

- **git diff --cached**  
  Show differences between staged changes and the last commit.

- **git diff HEAD~1**  
  Show differences between current state and one commit ago.

- **git diff branch1..branch2**  
  Show differences between two branches.

## Security Commands
- **git config --global core.hooksPath /dev/null**  
  Disable Git hooks globally for security.

- **git config --global safe.directory "*"**  
  Allow all directories as safe.

- **git fsck --full**  
  Check repository integrity for security issues.

- **git log --all --grep="password\|secret"**  
  Search commit history for sensitive data.
