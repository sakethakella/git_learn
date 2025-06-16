# Git & GitHub Complete Guide for Windows

A comprehensive guide to Git version control and GitHub collaboration specifically for Windows users.

## Table of Contents

- [What is Git?](#what-is-git)
- [What is GitHub?](#what-is-github)
- [Windows Installation](#windows-installation)
- [Initial Setup](#initial-setup)
- [Basic Git Commands](#basic-git-commands)
- [Working with Branches](#working-with-branches)
- [Remote Repositories](#remote-repositories)
- [GitHub Workflow](#github-workflow)
- [Advanced Git Commands](#advanced-git-commands)
- [Windows-Specific Tips](#windows-specific-tips)
- [Git Best Practices](#git-best-practices)
- [Common Scenarios](#common-scenarios)
- [Troubleshooting](#troubleshooting)

## What is Git?

Git is a distributed version control system that tracks changes in files and coordinates work among multiple people. It allows you to:

- Track file changes over time
- Revert to previous versions
- Work on different features simultaneously
- Collaborate with others without conflicts
- Maintain a complete history of your project

## What is GitHub?

GitHub is a cloud-based hosting service for Git repositories. It provides:

- Remote storage for your Git repositories
- Collaboration tools (pull requests, issues, discussions)
- Project management features
- CI/CD integration
- Documentation hosting (GitHub Pages)

## Windows Installation

### Step 1: Download Git for Windows

1. Visit [git-scm.com](https://git-scm.com/)
2. Click "Download for Windows"
3. The download will start automatically

### Step 2: Install Git

1. Run the downloaded `.exe` file
2. **Recommended installation options:**
   - **Select Components:** Check "Git Bash Here" and "Git GUI Here"
   - **Default Editor:** Choose your preferred editor (VS Code recommended)
   - **PATH Environment:** Select "Git from the command line and also from 3rd-party software"
   - **HTTPS Transport:** Use the OpenSSL library
   - **Line Ending Conversions:** "Checkout Windows-style, commit Unix-style line endings"
   - **Terminal Emulator:** Use MinTTY
   - **Git Pull Behavior:** Default (fast-forward or merge)
   - **Credential Helper:** Git Credential Manager Core
   - **Extra Options:** Enable file system caching

### Step 3: Verify Installation

Open Command Prompt or PowerShell and run:

```cmd
git --version
```

### Available Interfaces on Windows

- **Git Bash:** Unix-like terminal (recommended for Git commands)
- **Command Prompt:** Windows native terminal
- **PowerShell:** Enhanced Windows terminal
- **Git GUI:** Graphical interface for Git operations

## Initial Setup

Configure your identity (required for commits). Open Git Bash, Command Prompt, or PowerShell:

```bash
# Set your name and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name
git config --global init.defaultBranch main

# Set default editor (Windows options)
git config --global core.editor "code --wait"        # VS Code
git config --global core.editor "notepad"            # Notepad
git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"  # Notepad++

# Configure line endings for Windows
git config --global core.autocrlf true

# View your configuration
git config --list

# View specific configuration
git config user.name
git config user.email
```

### Windows-Specific Configuration

```bash
# Set credential helper (usually set during installation)
git config --global credential.helper manager-core

# Configure file permissions (Windows doesn't track execute permissions)
git config --global core.filemode false

# Configure safe directory (if needed for shared drives)
git config --global --add safe.directory '*'
```

## Basic Git Commands

### Repository Initialization

```bash
# Create a new repository
git init

# Clone an existing repository
git clone https://github.com/username/repository-name.git
git clone git@github.com:username/repository-name.git  # SSH
```

### File Operations

```bash
# Check repository status
git status

# Add files to staging area
git add filename.txt           # Add specific file
git add .                      # Add all files
git add *.js                   # Add all JavaScript files
git add src/                   # Add all files in src directory

# Remove files from staging area
git reset filename.txt         # Unstage specific file
git reset                      # Unstage all files

# Commit changes
git commit -m "Your commit message"
git commit -am "Add and commit in one step"  # For tracked files only

# View commit history
git log
git log --oneline             # Compact view
git log --graph               # Show branch graph
git log -n 5                  # Show last 5 commits
```

### File Status and Differences

````bash
# Show differences
## Git Best Practices

### Commit Messages
```bash
# Good commit message format:
# <type>: <subject>
#
# <body>
#
# <footer>

# Examples:
git commit -m "feat: add user authentication"
git commit -m "fix: resolve login button alignment issue"
git commit -m "docs: update README with installation instructions"

# Types: feat, fix, docs, style, refactor, test, chore
````

### Branching Strategy

```bash
# Use descriptive branch names
git checkout -b feature/user-authentication
git checkout -b bugfix/login-form-validation
git checkout -b hotfix/security-patch

# Keep branches focused on single features
# Delete merged branches to keep repository clean
```

### General Best Practices

- Commit often, push regularly
- Write meaningful commit messages
- Review changes before committing (`git diff`)
- Use `.gitignore` to exclude unnecessary files
- Keep commits atomic (one logical change per commit)
- Test before pushing to shared branches
- Use pull requests for code review

## Common Scenarios

### Starting a New Project

```bash
# Method 1: Start locally
mkdir my-project
cd my-project
git init
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"
git remote add origin https://github.com/username/my-project.git
git push -u origin main

# Method 2: Start on GitHub
# 1. Create repository on GitHub
# 2. Clone it locally
git clone https://github.com/username/my-project.git
cd my-project
```

### Contributing to Open Source

```bash
# 1. Fork the repository on GitHub
# 2. Clone your fork
git clone https://github.com/yourusername/project.git
cd project

# 3. Add upstream remote
git remote add upstream https://github.com/originalowner/project.git

# 4. Create feature branch
git checkout -b feature/improvement

# 5. Make changes, commit, and push
git add .
git commit -m "Add improvement feature"
git push origin feature/improvement

# 6. Create pull request on GitHub
# 7. Keep your fork updated
git checkout main
git pull upstream main
git push origin main
```

### Handling Merge Conflicts (Windows)

```bash
# When conflicts occur during merge
git merge feature-branch
# Auto-merging file.txt
# CONFLICT (content): Merge conflict in file.txt

# Open conflicted file in your editor
# Look for conflict markers:
# <<<<<<< HEAD
# Your changes
# =======
# Their changes
# >>>>>>> feature-branch

# Resolve conflicts manually, then:
git add file.txt
git commit -m "Resolve merge conflict"
```

### Working with Large Files

```bash
# Install Git LFS (Large File Storage)
# Download from: https://git-lfs.github.io/

# Initialize LFS in repository
git lfs install

# Track large file types
git lfs track "*.psd"
git lfs track "*.zip"
git lfs track "*.exe"

# Add .gitattributes
git add .gitattributes
git commit -m "Add LFS tracking"

# Add and commit large files normally
git add large-file.zip
git commit -m "Add large file"
git push origin main
```

## Troubleshooting

### Common Windows Issues

#### Permission Errors

```bash
# Run Git Bash as Administrator if needed
# Or configure safe directories:
git config --global --add safe.directory '*'
```

#### Path Too Long Errors

```bash
# Enable long path support
git config --global core.longpaths true
```

#### Line Ending Issues

```bash
# Fix line ending configuration
git config --global core.autocrlf true

# Reset all files with correct line endings
git rm --cached -r .
git reset --hard
```

#### SSH Connection Issues

```bash
# Test SSH connection
ssh -T git@github.com

# Start SSH agent (Git Bash)
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Use HTTPS instead of SSH if needed
git remote set-url origin https://github.com/username/repository.git
```

### General Troubleshooting

```bash
# Check Git status
git status

# Check remote URLs
git remote -v

# Check configuration
git config --list

# Reset to last known good state
git reset --hard HEAD

# Clean untracked files
git clean -fd

# View detailed log
git log --oneline --graph --decorate --all
```

### Getting Help

```bash
# Built-in help
git help
git help command-name
git command-name --help

# Quick reference
git status
git log --oneline
```

## Useful Resources

- **Official Git Documentation:** [git-scm.com/doc](https://git-scm.com/doc)
- **GitHub Docs:** [docs.github.com](https://docs.github.com)
- **Interactive Git Tutorial:** [learngitbranching.js.org](https://learngitbranching.js.org)
- **Git Cheat Sheet:** [education.github.com/git-cheat-sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- **Atlassian Git Tutorials:** [atlassian.com/git/tutorials](https://www.atlassian.com/git/tutorials)

## Quick Reference Commands

```bash
# Repository setup
git init                      # Initialize repository
git clone <url>              # Clone repository

# Basic operations
git status                   # Check status
git add <file>               # Stage file
git commit -m "message"      # Commit changes
git push                     # Push to remote
git pull                     # Pull from remote

# Branching
git branch                   # List branches
git checkout -b <branch>     # Create and switch branch
git merge <branch>           # Merge branch

# Information
git log                      # View commit history
git diff                     # View changes
git remote -v                # View remotes
```

---

_This guide covers the essential Git and GitHub commands for Windows users. Practice these commands regularly to become proficient with version control!_

Branches allow you to work on different features simultaneously without affecting the main codebase.

```bash
# List branches
git branch                    # Local branches
git branch -r                 # Remote branches
git branch -a                 # All branches

# Create and switch to new branch
git checkout -b feature-name
git switch -c feature-name    # Modern alternative

# Switch between branches
git checkout main
git switch main               # Modern alternative

# Create branch without switching
git branch feature-name

# Delete branch
git branch -d feature-name    # Safe delete (only if merged)
git branch -D feature-name    # Force delete

# Rename current branch
git branch -m new-branch-name

# Merge branch into current branch
git merge feature-name

# Rebase current branch onto another
git rebase main
```

## Remote Repositories

### Adding and Managing Remotes

```bash
# Add remote repository
git remote add origin https://github.com/username/repository-name.git

# View remotes
git remote -v

# Change remote URL
git remote set-url origin https://github.com/username/new-repository.git

# Remove remote
git remote remove origin
```

### Pushing and Pulling Changes

```bash
# Push to remote repository
git push origin main          # Push main branch
git push origin feature-name  # Push specific branch
git push -u origin main       # Set upstream and push
git push --all               # Push all branches

# Pull changes from remote
git pull origin main         # Pull specific branch
git pull                     # Pull current branch

# Fetch changes without merging
git fetch origin
git fetch --all              # Fetch all remotes
```

## GitHub Workflow

### Setting up SSH Keys (Windows)

```bash
# Generate SSH key (in Git Bash)
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard (Git Bash)
cat ~/.ssh/id_ed25519.pub | clip

# Or manually copy from:
# C:\Users\YourUsername\.ssh\id_ed25519.pub
```

Add the copied key to your GitHub account: Settings → SSH and GPG keys → New SSH key

### Basic GitHub Workflow

```bash
# 1. Fork repository on GitHub (click Fork button)

# 2. Clone your fork
git clone git@github.com:yourusername/repository-name.git

# 3. Add upstream remote
git remote add upstream git@github.com:originaluser/repository-name.git

# 4. Create feature branch
git checkout -b feature-name

# 5. Make changes and commit
git add .
git commit -m "Add new feature"

# 6. Push to your fork
git push origin feature-name

# 7. Create Pull Request on GitHub

# 8. Keep your fork updated
git checkout main
git pull upstream main
git push origin main
```

## Advanced Git Commands

### Viewing History and Changes

```bash
# Advanced log options
git log --oneline --graph --all
git log --author="Author Name"
git log --since="2023-01-01"
git log --until="2023-12-31"
git log --grep="bug fix"
git log -p                   # Show patches/diffs

# Show specific commit
git show commit-hash

# Show file history
git log --follow filename.txt
```

### Undoing and Reverting

```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Undo specific file changes
git checkout -- filename.txt
git restore filename.txt     # Modern alternative

# Revert a commit (creates new commit)
git revert commit-hash

# Interactive rebase (edit commit history)
git rebase -i HEAD~3
```

### Stashing Changes

```bash
# Save current changes temporarily
git stash
git stash save "work in progress"

# List stashes
git stash list

# Apply stash
git stash apply              # Keep stash
git stash pop                # Apply and remove stash

# Apply specific stash
git stash apply stash@{2}

# Delete stash
git stash drop stash@{0}
git stash clear              # Delete all stashes
```

### Tags

```bash
# Create lightweight tag
git tag v1.0.0

# Create annotated tag
git tag -a v1.0.0 -m "Version 1.0.0"

# List tags
git tag
git tag -l "v1.*"

# Push tags
git push origin v1.0.0
git push origin --tags       # Push all tags

# Delete tag
git tag -d v1.0.0            # Local
git push origin --delete v1.0.0  # Remote
```

## Windows-Specific Tips

### Using Different Terminals

```bash
# Git Bash (recommended for Git operations)
# - Unix-like environment
# - Better Git integration
# - Supports SSH agent

# Command Prompt
# - Native Windows terminal
# - Limited features compared to Git Bash

# PowerShell
# - Enhanced Windows terminal
# - Good Git support with modules
# - Install Posh-Git for better experience:
# Install-Module posh-git -Scope CurrentUser
```

### File Path Considerations

```bash
# Windows uses backslashes, Git uses forward slashes
# Git automatically handles path conversion

# Avoid spaces in file/folder names when possible
# If needed, use quotes:
git add "file with spaces.txt"

# Long path support (Windows 10+)
git config --global core.longpaths true
```

### Line Ending Configuration

```bash
# Windows (CRLF) to Unix (LF) conversion
git config --global core.autocrlf true

# Check current setting
git config core.autocrlf

# If working only on Windows
git config --global core.autocrlf false
```

### GUI Tools for Windows

- **GitHub Desktop:** User-friendly GUI application
- **Git GUI:** Built-in with Git installation
- **SourceTree:** Advanced Git GUI by Atlassian
- **TortoiseGit:** Windows Explorer integration
- **GitKraken:** Commercial Git client with visual interface
