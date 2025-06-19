---
title: "Git Workflow Cheatsheet"
date: 2024-01-10
tags: ["git", "cheatsheet", "workflow"]
category: "cheatsheets"
references:
  - title: "Git Documentation"
    url: "https://git-scm.com/docs"
  - title: "Atlassian Git Tutorials"
    url: "https://www.atlassian.com/git/tutorials"
---

# Git Workflow Cheatsheet

Quick reference for common Git operations and workflows.

## Basic Commands

```bash
# Initialize repository
git init

# Clone repository
git clone <url>

# Check status
git status

# Add files
git add <file>
git add .  # Add all files

# Commit changes
git commit -m "Commit message"
git commit -am "Add and commit in one step"
```

## Branch Management

```bash
# List branches
git branch
git branch -r  # Remote branches
git branch -a  # All branches

# Create branch
git branch <branch-name>
git checkout -b <branch-name>  # Create and switch

# Switch branches
git checkout <branch-name>
git switch <branch-name>  # Modern alternative

# Delete branch
git branch -d <branch-name>
git branch -D <branch-name>  # Force delete
```

## Remote Operations

```bash
# Add remote
git remote add origin <url>

# Push changes
git push origin <branch-name>
git push -u origin <branch-name>  # Set upstream

# Pull changes
git pull origin <branch-name>
git pull --rebase  # Rebase instead of merge

# Fetch changes
git fetch origin
```

## Merge vs Rebase

```bash
# Merge feature branch to main
git checkout main
git merge feature-branch

# Rebase feature branch onto main
git checkout feature-branch
git rebase main

# Interactive rebase (clean up commits)
git rebase -i HEAD~3
```

## Useful Aliases

Add to your `~/.gitconfig`:

```ini
[alias]
  st = status
  co = checkout
  br = branch
  ci = commit
  ca = commit -am
  unstage = reset HEAD --
  last = log -1 HEAD
  visual = !gitk
  lg = log --oneline --graph --decorate
```

## Common Scenarios

### Undo Last Commit (Keep Changes)
```bash
git reset --soft HEAD~1
```

### Undo Last Commit (Discard Changes)
```bash
git reset --hard HEAD~1
```

### Stash Work in Progress
```bash
git stash
git stash pop
git stash list
git stash drop
```

### Cherry Pick Commit
```bash
git cherry-pick <commit-hash>
```

## Best Practices

1. **Write descriptive commit messages**
2. **Use feature branches for new work**
3. **Pull before pushing**
4. **Keep commits atomic and focused**
5. **Use `.gitignore` appropriately**
6. **Regular backups with remotes**