# 8. Git Security Best Practices

Security is crucial when working with Git repositories, especially in collaborative environments. This section covers essential security practices, recent vulnerabilities, and how to protect your repositories.

---

## Recent Security Vulnerabilities

### CVE-2025-48384: Submodule Configuration Vulnerability

**What it is:** A significant Git vulnerability affecting submodule configurations that could allow malicious code execution.

**Mitigation Steps:**
1. **Avoid recursive submodule clones from untrusted sources:**
   ```bash
   # Instead of:
   git clone --recurse-submodules <untrusted-repo>
   
   # Use:
   git clone <repo>
   git submodule init
   git submodule update
   ```

2. **Disable Git hooks globally:**
   ```bash
   git config --global core.hooksPath /dev/null
   ```

3. **Audit all submodules:**
   ```bash
   git submodule status
   ```
   Verify that all submodules are from trusted sources.

4. **Use specific submodule URLs:**
   Always use HTTPS URLs with specific commit hashes when possible.

---

## Repository Security Best Practices

### Authentication and Access Control

**Use SSH Keys:**
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Add to SSH agent
ssh-add ~/.ssh/id_ed25519
```

**Configure Git to use SSH:**
```bash
git config --global url."git@github.com:".insteadOf "https://github.com/"
```

### Secure Configuration

**Set up secure defaults:**
```bash
# Disable credential caching for sensitive repos
git config --global credential.helper cache --timeout=3600

# Use HTTPS for all operations
git config --global url."https://".insteadOf "git://"

# Disable automatic credential storage
git config --global credential.helper ""
```

**Configure safe defaults:**
```bash
# Prevent accidental commits to main branch
git config --global init.defaultBranch main

# Set up safe directory patterns
git config --global safe.directory "*"

# Disable automatic line ending conversion
git config --global core.autocrlf false
```

---

## Commit Security

### Signing Commits

**Set up GPG signing:**
```bash
# Generate GPG key
gpg --full-generate-key

# Configure Git to sign commits
git config --global user.signingkey <your-gpg-key-id>
git config --global commit.gpgsign true
```

**Verify signed commits:**
```bash
git log --show-signature
```

### Secure Commit Messages

**Use conventional commits:**
```bash
git commit -m "feat: add user authentication

- Implement secure password hashing
- Add two-factor authentication
- Update security documentation

Closes #123"
```

**Avoid sensitive information in commits:**
- Never commit passwords, API keys, or tokens
- Use environment variables or configuration files
- Add sensitive files to `.gitignore`

---

## Branch Protection

### Branch Protection Rules

**Set up branch protection:**
```bash
# Require pull request reviews
git config branch.main.protect true

# Require status checks
git config branch.main.requiredStatusChecks true

# Prevent force pushes
git config branch.main.denyNonFastForwards true
```

### Secure Branch Naming

**Use descriptive branch names:**
```bash
# Good examples:
git switch -c feature/user-authentication
git switch -c fix/security-vulnerability-123
git switch -c hotfix/critical-security-patch

# Avoid:
git switch -c temp
git switch -c test
git switch -c fix
```

---

## File and Directory Security

### .gitignore Best Practices

**Create comprehensive .gitignore:**
```bash
# Create .gitignore
cat > .gitignore << EOF
# Environment variables
.env
.env.local
.env.production

# API keys and secrets
config/secrets.yml
*.key
*.pem

# Logs
*.log
logs/

# Dependencies
node_modules/
vendor/

# IDE files
.vscode/
.idea/
*.swp
*.swo

# OS files
.DS_Store
Thumbs.db
EOF
```

### Secure File Handling

**Check for sensitive data before committing:**
```bash
# Search for potential secrets
git grep -n "password\|secret\|key\|token" --cached

# Use git-secrets tool
git secrets --install
git secrets --register-aws
```

---

## Remote Repository Security

### Secure Remote URLs

**Use HTTPS with authentication:**
```bash
# Instead of:
git remote add origin git@github.com:user/repo.git

# Use:
git remote add origin https://github.com/user/repo.git
```

**Verify remote URLs:**
```bash
git remote -v
```

### Secure Cloning

**Clone with specific protocols:**
```bash
# Use HTTPS
git clone https://github.com/user/repo.git

# Verify repository integrity
git fsck --full
```

---

## Audit and Monitoring

### Repository Auditing

**Check repository integrity:**
```bash
# Verify repository integrity
git fsck --full

# Check for unreachable objects
git fsck --unreachable

# Verify all objects
git cat-file --batch-check --batch-all-objects
```

**Audit commit history:**
```bash
# Check for large files
git rev-list --objects --all | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | awk '/^blob/ {print substr($0,6)}' | sort --numeric-sort --key=2

# Check for sensitive data in history
git log --all --full-history -- "*.env" "*.key" "*.pem"
```

### Access Monitoring

**Monitor repository access:**
```bash
# Check recent activity
git reflog

# Monitor branch changes
git log --oneline --graph --all --since="1 week ago"
```

---

## Emergency Response

### Security Incident Response

**If a security incident occurs:**

1. **Immediately revoke access:**
   ```bash
   # Remove compromised credentials
   git config --unset credential.helper
   ```

2. **Audit recent changes:**
   ```bash
   git log --oneline --since="1 day ago"
   git reflog --since="1 day ago"
   ```

3. **Check for unauthorized commits:**
   ```bash
   git log --all --grep="unauthorized\|suspicious"
   ```

4. **Verify repository integrity:**
   ```bash
   git fsck --full
   ```

### Recovery Procedures

**Restore from backup:**
```bash
# If you have a clean backup
git reset --hard <clean-commit-hash>

# Force push to remote (use with extreme caution)
git push --force-with-lease origin main
```

---

## Additional Security Tools

### Git Hooks for Security

**Pre-commit hook example:**
```bash
#!/bin/sh
# Check for sensitive data
if git diff --cached --name-only | xargs grep -l "password\|secret\|key"; then
    echo "Error: Sensitive data detected in staged files"
    exit 1
fi
```

### Third-party Security Tools

- **git-secrets:** Prevents committing secrets
- **truffleHog:** Scans for secrets in Git history
- **git-crypt:** Encrypts sensitive files in Git
- **BFG Repo-Cleaner:** Removes sensitive data from Git history

---

## Summary

Security in Git is an ongoing process that requires:

1. **Regular updates** to Git and related tools
2. **Proper configuration** of authentication and access controls
3. **Consistent practices** for handling sensitive data
4. **Regular auditing** of repository integrity and access
5. **Emergency response plans** for security incidents

By following these practices, you can significantly improve the security of your Git repositories and protect your code and data from unauthorized access or malicious activities.
