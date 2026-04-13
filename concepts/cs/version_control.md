# Structure

### Working Directory

Holds the actual files

### Index

Acts as a staging area

### HEAD

Points to the last commit you’ve made

# Commands

```bash
# Create a new git repository in current directory
git init

# Create a working copy of a repository
git clone /path/to/repo

# Propose changes (add it to the index)
git add <filename>
git add *

# Commit proposed changes to HEAD
git commit -m "Commit message"

# Send committed changes to remote repository
git push origin <branch>

# Create a new branch and switch to it
git checkout -b <branch>

# Switch back to dev branch
git checkout dev

# Delete a branch
git branch -d <branch>

# Update local repository (fetches and merges remote changes)
git pull

# Update local repository with submodules
git submodule update --init --recursive

# Merge a branch into the active branch
git merge <branch>

# Edit conflicting files and mark as merged
git add <filename>

# Preview changes before merging
git diff <source_branch> <target_branch>

# See commit history
git log # --author=bob # --pretty=oneline

# Replace local changes
git checkout -- <filename>

# Drop all local changes and commits, fetch latest history, and point local at dev
git fetch origin
git reset --hard origin/master
```

# Workflow

### Clone a new repo

```bash
# Repo without submodules
git clone repo_url

# Repo with submodules
git clone --recurse-submodules repo_url
```

### Checkout a new branch

```bash
# 1. Update original branch
git pull
git submodule update --init --recursive

# 2. Checkout new branch
git checkout -b PR-00000
```

### Checkout an existing branch

```bash
# 1. Update original branch
git checkout PR-00000
git pull
git submodule update --init --recursive

# 2. CHeckout remote branch
git checkout PR-00001

# 3. Update submodules
git submodule update --init --recursive
```

### Update Changes

```bash
# 1. Stage changes changes
git add <filename>

# 2. Add commit
git commit -m "Commit Message"

# 3. Push to remote repo
git push origin <branch>
```
### Git Keeping but Ignoring Data
Add `data/.gitkeep`
Add `data/` to `.gitignore`