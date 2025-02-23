## 6. Git Cheat Sheet

### Git Basics
- **git init**  
  Initialize a new Git repository.

- **git status**  
  Display the state of the working directory and staging area.

- **git add .**  
  Stage all new and modified files (excluding deletions).

- **git add -A**  
  Stage all changes, including deletions.

- **git commit -m "message"**  
  Commit staged changes with a short message.

- **git commit**  
  Open the default editor to write a detailed commit message.

- **git log --oneline**  
  Show commit history in a one-line format.

- **git log --oneline --graph**  
  Display a commit graph alongside the one-line log.

---

### Branching and Merging
- **git branch**  
  List all local branches.

- **git checkout -b branch-name**  
  Create a new branch and switch to it.

- **git checkout branch-name**  
  Switch to an existing branch.

- **git merge branch-name**  
  Merge the specified branch into the current branch.

- **git rebase branch-name**  
  Rebase the current branch onto the specified branch for a linear history.

- **git branch -d branch-name**  
  Delete the specified branch (only if it has been merged).

---

### Remote Repositories
- **git remote add origin <repo-url>**  
  Add a remote repository and name it `origin`.

- **git remote -v**  
  List all remote repositories and their URLs.

- **git push -u origin branch-name**  
  Push the branch to `origin` and set it as the default upstream branch.

- **git pull**  
  Fetch and merge changes from the remote repository.

- **git fetch**  
  Fetch new commits from the remote without merging.

- **git clone <repo-url>**  
  Clone a remote repository to your local machine.

---

### Undoing Changes
- **git revert <commit-hash>**  
  Create a new commit that undoes the changes of a specified commit.

- **git reset --soft HEAD~1**  
  Move HEAD to the previous commit, keeping changes staged.

- **git reset --mixed HEAD~1**  
  Reset to the previous commit and unstage changes (default mode).

- **git reset --hard HEAD~1**  
  Reset to the previous commit and discard all changes (use with caution).

- **git restore <file>**  
  Revert changes in a file back to the last committed state.

- **git restore --staged <file>**  
  Unstage a file while keeping its modifications in the working directory.

---

### Advanced Git
- **git stash**  
  Temporarily save uncommitted changes.

- **git stash list**  
  List all saved stashes.

- **git stash apply**  
  Reapply the latest stash without removing it from the stash list.

- **git stash pop**  
  Reapply the latest stash and remove it from the stash list.

- **git cherry-pick <commit-hash>**  
  Apply a specific commit from another branch onto the current branch.

- **git bisect start**  
  Begin a binary search to find the commit that introduced a bug.

- **git bisect bad/good**  
  Mark commits as bad or good during the bisect process.

- **git bisect reset**  
  End the bisect session and return to the original branch.

---

### Additional Commands
- **git config --global user.name "Your Name"**  
  Set your global Git username.

- **git config --global user.email "youremail@example.com"**  
  Set your global Git email.

- **git diff**  
  Display differences between commits, branches, or the working directory.
