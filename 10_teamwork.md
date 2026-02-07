# Professional Git Pull Request Workflow

A practical, real‑world guide to reviewing pull requests like an engineer on a production team.

This is not "Git commands memorization." This is about building the correct mental model so nothing feels magical.

---

# The Core Idea

A pull request is simply:

> "Here is a branch. Please merge these commits into main."

Everything else (GitHub UI, buttons, reviews) is just decoration around that simple truth.

Git itself only knows **branches and commits**.

---

# Part 1 — What `git fetch` REALLY does

## The mental model

Your computer does **not automatically know** what changed on GitHub.

You have:

* local branches → `main`, `feature-x`
* remote-tracking branches → `origin/main`

Think of `origin/main` as:

> "My last downloaded snapshot of GitHub's main"

It can be stale.

---

## Before fetch

Someone pushed commits to GitHub:

```
GitHub main: A — B — C — D — E
Your main:   A — B — C
```

You literally don't have D and E yet.

---

## Run

```bash
git fetch origin
```

One-line meaning: download new commits without touching my work.

---

## After fetch

```
main:        A — B — C
origin/main: A — B — C — D — E
```

Your files didn't change.
Your branch didn't change.
Only knowledge changed.

This is why professionals fetch first.

Knowledge first. Merging later.

---

# Why not `git pull`?

```
git pull = fetch + merge
```

That means surprise changes to your branch.

During reviews or debugging, surprise merges are chaos.

So:

* reviewing → fetch
* syncing your branch → pull

---

# Part 2 — Reviewing a Pull Request Locally

Serious review means running the code.
GitHub UI is only for quick reading.

If logic matters, always check locally.

---

## Case A — Internal team branch

Teammate pushes:

```
feature/login-fix
```

### Step 1 — update knowledge

```bash
git fetch origin
```

Downloads the branch.

### Step 2 — create safe local copy

```bash
git checkout -b pr-login origin/feature/login-fix
```

Meaning:

* create branch named pr-login
* base it on remote branch

Now you can:

* run tests
* debug
* add logs
* break things safely

Your `main` stays clean.

Think of this as a sandbox.

---

## Case B — External contributor (fork PR)

Contributor does NOT push to your repo.
They push to their fork.

GitHub exposes the PR like a hidden branch:

```
pull/<number>/head
```

### Fetch it

```bash
git fetch origin pull/123/head:pr-123
```

Meaning:

* download PR #123
* save it locally as branch pr-123

### Checkout

```bash
git checkout pr-123
```

Now it behaves like a normal branch.

No magic. Just another ref.

---

# What to actually review

Run the project like a user would.

Examples:

```
npm install
npm test
npm run dev
```

Then read the code slowly.

Ask yourself:

* Does this break edge cases?
* Is this simpler than needed?
* Are errors handled?
* Are tests missing?

If you can't explain the change in one sentence, it's probably too complex.

---

# Part 3 — Merge Strategies Explained Visually

History design matters more than people think.

---

## 1. Squash and Merge (most common)

Before:

```
feature: A — B — C
main:    D
```

After:

```
main: D — S
```

S = combined commit

### Effect

All small messy commits become one clean commit.

### When to use

* small teams
* startups
* features like "add login endpoint"

### Why it's nice

Easy revert:

```
git revert S
```

One commit, gone.

---

## 2. Rebase and Merge

Before:

```
main:    A — B
feature:     C — D
```

After:

```
main: A — B — C — D
```

Commits replay on top.

### Effect

Perfect straight line.

Looks like you wrote everything directly on main.

### When to use

* clean history obsessed teams
* libraries
* experienced developers

### Risk

Rewrites history if misused.

---

## 3. Merge Commit

Before:

```
main:    A — B
feature:     C — D
```

After:

```
main: A — B -------- M
             \------ C — D
```

### Effect

Keeps the true branch structure.

### When to use

* big teams
* long features
* enterprise repos

### Downside

History becomes messy fast.

---

# Recommended Default

If you are unsure:

Use **Squash and merge**.

It keeps life simple.

Simple history beats clever history.

---

# Professional PR Review Flow (what real teams do)

1. Read PR on GitHub
2. Fetch
3. Checkout locally
4. Run tests/app
5. Review code
6. Comment or request changes
7. Merge (usually squash)
8. Delete review branch

---

# Tiny Example Walkthrough

PR #42 adds "reset password".

```
git fetch origin
git fetch origin pull/42/head:pr-42
git checkout pr-42
npm test
npm run dev
```

You try resetting password manually.

Bug appears → comment → request changes.

That's real engineering. Not clicking buttons.

---

# Final Mental Model

Git is not complicated.

It only has:

* commits
* branches
* pointers

Everything else is workflow discipline.

If you always:

* fetch first
* review locally
* merge cleanly

You already behave like a professional developer.

