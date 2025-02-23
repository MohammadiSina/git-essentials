## 3. Working with Remote Repositories

### Connecting to a Remote Repository

**Command:**
```bash
git remote add origin <repo-url>
```
**What it does:** Links your local repository to a remote repository (often hosted on platforms like GitHub, GitLab, or Bitbucket).

**Example:**
```bash
git remote add origin https://github.com/yourusername/my-project.git
```
This command sets the remote named `origin` to point to your online repository.

**Exercise:**
1. Create a remote repository on GitHub (or another platform).
2. In your local project, add the remote using the above command.
3. Verify the remote is added by running:
   ```bash
   git remote -v
   ```

---

### Pushing Code to a Remote Repository

**Command:**
```bash
git push -u origin master
```
**What it does:** Pushes the local `master` branch to the remote named `origin` and sets it as the default upstream branch by using the `-u` flag. This makes future pushes and pulls simpler since you won’t need to specify the branch. If the online repository doesn't have a branch by your local repository name, it would be created automatically.


**Exercise:**
1. After adding a few commits locally, push your code to the remote repository using the above command.
2. Check your remote repository on GitHub to confirm your changes.

---

### Cloning a Repository

**Command:**
```bash
git clone <repo-url>
```
**What it does:** Creates a local copy of an existing remote repository.

**Example:**
```bash
git clone https://github.com/yourusername/my-project.git
```

**Exercise:**
1. Clone an existing repository from GitHub to a new directory on your machine.
2. Navigate into the cloned repository to see the initial state and run:
   ```bash
   git status
   ```

---

### Fetching and Pulling Remote Changes

#### Fetching Changes

**Command:**
```bash
git fetch
```
**What it does:** Downloads new commits from the remote repository but does not merge them into your current branch. This allows you to review changes before integrating them.

**Exercise:**
1. Run `git fetch` in your repository.
2. Use `git log --oneline --graph --all` to view the fetched changes.

#### Pulling Changes

**Command:**
```bash
git pull
```
**What it does:** Fetches new commits from the remote repository and automatically merges them into your current branch.


**Exercise:**
1. After someone else pushes changes to the remote repository, run `git pull` to update your local branch.
2. Verify that your local branch reflects the latest changes.