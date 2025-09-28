# 9. Modern Git Workflows

This section covers modern Git workflows and best practices used in professional development environments. These workflows help teams collaborate effectively while maintaining code quality and project history.

---

## Git Flow

Git Flow is a branching model that defines a strict branching structure designed around project releases.

### Branch Types

- **main**: Production-ready code
- **develop**: Integration branch for features
- **feature/**: Feature development branches
- **release/**: Release preparation branches
- **hotfix/**: Critical production fixes

### Workflow Steps

1. **Start a new feature:**
   ```bash
   git switch develop
   git pull origin develop
   git switch -c feature/new-feature
   ```

2. **Work on the feature:**
   ```bash
   # Make changes and commit
   git add .
   git commit -m "feat: add new feature functionality"
   ```

3. **Finish the feature:**
   ```bash
   git switch develop
   git pull origin develop
   git merge --no-ff feature/new-feature
   git push origin develop
   git branch -d feature/new-feature
   ```

4. **Create a release:**
   ```bash
   git switch -c release/1.0.0
   # Make release-specific changes
   git commit -m "chore: bump version to 1.0.0"
   git switch main
   git merge --no-ff release/1.0.0
   git tag -a v1.0.0 -m "Release version 1.0.0"
   git push origin main --tags
   ```

---

## GitHub Flow

A simpler workflow focused on continuous deployment, popular in modern web development.

### Branch Types

- **main**: Always deployable
- **feature/**: Feature development branches

### Workflow Steps

1. **Create a feature branch:**
   ```bash
   git switch main
   git pull origin main
   git switch -c feature/user-authentication
   ```

2. **Develop and commit:**
   ```bash
   # Make changes
   git add .
   git commit -m "feat: implement user login"
   
   # Push to remote
   git push -u origin feature/user-authentication
   ```

3. **Create a Pull Request:**
   - Open a PR on GitHub/GitLab
   - Request code review
   - Address feedback

4. **Merge after approval:**
   ```bash
   git switch main
   git pull origin main
   git merge feature/user-authentication
   git push origin main
   git branch -d feature/user-authentication
   ```

---

## Trunk-Based Development

A workflow where developers work on short-lived branches or directly on the main branch.

### Branch Strategy

- **main**: Primary development branch
- **feature/**: Short-lived feature branches (1-2 days max)

### Workflow Steps

1. **Start from main:**
   ```bash
   git switch main
   git pull origin main
   ```

2. **Create a small feature branch:**
   ```bash
   git switch -c feature/small-change
   ```

3. **Make atomic commits:**
   ```bash
   git add .
   git commit -m "feat: add input validation"
   ```

4. **Quick merge back:**
   ```bash
   git switch main
   git merge feature/small-change
   git push origin main
   git branch -d feature/small-change
   ```

---

## Conventional Commits

A specification for writing clear and consistent commit messages.

### Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Types

- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation changes
- **style**: Code style changes (formatting, etc.)
- **refactor**: Code refactoring
- **test**: Adding or updating tests
- **chore**: Maintenance tasks

### Examples

```bash
git commit -m "feat(auth): add two-factor authentication

- Implement TOTP generation
- Add QR code display
- Update user settings UI

Closes #123"

git commit -m "fix: resolve memory leak in image processing

The issue was caused by not properly disposing of image objects
after processing. This fix ensures proper cleanup.

Fixes #456"

git commit -m "docs: update API documentation

- Add examples for new endpoints
- Fix typos in parameter descriptions
- Update version compatibility matrix"
```

---

## Branch Protection Rules

Configure branch protection to enforce code quality and review processes.

### GitHub Branch Protection

1. **Navigate to repository settings**
2. **Go to Branches section**
3. **Add rule for main branch:**
   - Require pull request reviews
   - Require status checks
   - Require up-to-date branches
   - Restrict pushes to matching branches

### GitLab Branch Protection

1. **Go to Repository > Branches**
2. **Set up branch protection:**
   - Allowed to merge: Maintainers
   - Allowed to push: No one
   - Require approval from code owners

---

## Code Review Best Practices

### For Authors

1. **Keep PRs small and focused:**
   - One feature per PR
   - Maximum 400 lines of changes
   - Clear, descriptive titles

2. **Write good PR descriptions:**
   ```markdown
   ## What
   Brief description of changes

   ## Why
   Explanation of why these changes are needed

   ## How
   High-level overview of implementation

   ## Testing
   How to test these changes

   ## Screenshots
   If applicable, include before/after screenshots
   ```

3. **Use draft PRs for work in progress:**
   ```bash
   # Create draft PR
   gh pr create --draft
   ```

### For Reviewers

1. **Review checklist:**
   - [ ] Code follows project conventions
   - [ ] Tests are included and passing
   - [ ] Documentation is updated
   - [ ] No security vulnerabilities
   - [ ] Performance implications considered

2. **Provide constructive feedback:**
   - Be specific about issues
   - Suggest improvements
   - Acknowledge good practices

---

## Continuous Integration/Continuous Deployment

### GitHub Actions Example

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
    - name: Install dependencies
      run: npm ci
    - name: Run tests
      run: npm test
    - name: Run linting
      run: npm run lint

  security:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Run security audit
      run: npm audit --audit-level moderate
```

### GitLab CI Example

```yaml
stages:
  - test
  - security
  - deploy

test:
  stage: test
  script:
    - npm ci
    - npm test
    - npm run lint

security:
  stage: security
  script:
    - npm audit --audit-level moderate

deploy:
  stage: deploy
  script:
    - echo "Deploying to production"
  only:
    - main
```

---

## Release Management

### Semantic Versioning

Follow semantic versioning (SemVer) for releases: `MAJOR.MINOR.PATCH`

- **MAJOR**: Breaking changes
- **MINOR**: New features (backward compatible)
- **PATCH**: Bug fixes (backward compatible)

### Creating Releases

1. **Update version numbers:**
   ```bash
   # Update package.json
   npm version patch  # or minor, major
   ```

2. **Create release notes:**
   ```bash
   # Generate changelog
   git log --oneline v1.0.0..HEAD > CHANGELOG.md
   ```

3. **Tag the release:**
   ```bash
   git tag -a v1.1.0 -m "Release version 1.1.0"
   git push origin v1.1.0
   ```

4. **Create GitHub release:**
   ```bash
   gh release create v1.1.0 --notes-file CHANGELOG.md
   ```

---

## Conflict Resolution

### Preventing Conflicts

1. **Keep branches up to date:**
   ```bash
   git switch main
   git pull origin main
   git switch feature-branch
   git rebase main
   ```

2. **Communicate with team:**
   - Discuss large changes before implementing
   - Coordinate on shared files
   - Use feature flags for incomplete features

### Resolving Conflicts

1. **Identify conflicted files:**
   ```bash
   git status
   ```

2. **Open files and resolve conflicts:**
   ```bash
   # Look for conflict markers
   <<<<<<< HEAD
   Your changes
   =======
   Their changes
   >>>>>>> branch-name
   ```

3. **Stage resolved files:**
   ```bash
   git add resolved-file.txt
   ```

4. **Complete the merge/rebase:**
   ```bash
   git commit  # for merge
   # or
   git rebase --continue  # for rebase
   ```

---

## Best Practices Summary

### General Guidelines

1. **Commit often, push regularly**
2. **Write clear, descriptive commit messages**
3. **Keep commits atomic and focused**
4. **Use branches for all changes**
5. **Review code before merging**
6. **Test before pushing**

### Security Considerations

1. **Never commit secrets or credentials**
2. **Use .gitignore effectively**
3. **Review all changes for security issues**
4. **Keep dependencies updated**
5. **Use signed commits for important changes**

### Performance Tips

1. **Use shallow clones for CI/CD**
2. **Enable Git maintenance**
3. **Clean up old branches regularly**
4. **Use Git LFS for large files**
5. **Optimize .gitignore patterns**

---

This workflow guide provides a foundation for modern Git practices. Choose the workflow that best fits your team's needs and project requirements.
