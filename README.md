#### This project is for the Devops bootcamp exercise for "Version Control" 
# DevOps Bootcamp - Version Control with Git Exercises

This project contains exercises for practicing Git version control commands and workflows.

## Prerequisites
- Git installed on your machine
- GitHub account
- Basic understanding of command line

## Exercise Solutions Guide

### EXERCISE 1: Clone and create new repository

*Objective:* Clone git repository, creating a new local copy and push it to your own Github remote repository.

bash
# 1. Clone the original repository
git clone <original-repository-url>
cd git-exercises-main

# 2. Create a new repository on GitHub (via web interface)

# 3. Change remote origin to your new repository
git remote remove origin
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# 4. Push to your new remote repository
git push -u origin main


### EXERCISE 2: .gitignore

*Objective:* Ignore .idea folder, .DS_Store, and build folders

bash
# 1. Create .gitignore file
echo "# IDE files
.idea/
.DS_Store

# Build folders
build/
.gradle/" > .gitignore

# 2. Remove already tracked files from git cache
git rm -r --cached .idea/ 2>/dev/null || true
git rm --cached .DS_Store 2>/dev/null || true
git rm -r --cached build/ 2>/dev/null || true
git rm -r --cached .gradle/ 2>/dev/null || true

# 3. Add and commit changes
git add .gitignore
git commit -m "Add .gitignore to exclude IDE and build files"
git push


### EXERCISE 3: Feature branch

*Objective:* Create a feature branch and make changes

bash
# 1. Create and switch to feature branch
git checkout -b feature/upgrade-dependencies

# 2. Upgrade logstash-logback-encoder version to 7.3
# Edit build.gradle file and change:
# implementation group: 'net.logstash.logback', name: 'logstash-logback-encoder', version: '7.3'

# 3. Add image to index.html
# Edit src/main/webapp/index.html and add:
# <img src="https://www.careeraddict.com/uploads/article/58721/illustration-group-people-team-meeting.jpg" alt="Team Meeting">

# 4. Check changes
git diff

# 5. Add and commit changes
git add .
git commit -m "Upgrade logstash-logback-encoder to version 7.3 and add team meeting image to index.html"

# 6. Push feature branch
git push -u origin feature/upgrade-dependencies


### EXERCISE 4: Bugfix branch

*Objective:* Create bugfix branch and fix spelling error

bash
# 1. Create and switch to bugfix branch (from main)
git checkout main
git checkout -b bugfix/spelling-correction

# 2. Fix spelling error in Application.java
# Edit src/main/java/com/example/Application.java and fix any spelling mistakes

# 3. Check changes
git diff

# 4. Commit changes
git add .
git commit -m "Fix spelling error in Application.java"

# 5. Push bugfix branch
git push -u origin bugfix/spelling-correction


### EXERCISE 5: Merge request

*Objective:* Merge feature branch into master using a merge request

bash
# 1. Go to GitHub web interface
# 2. Create Pull Request from feature/upgrade-dependencies to main
# 3. Review changes and merge via GitHub interface
# OR merge locally:

git checkout main
git merge feature/upgrade-dependencies
git push


### EXERCISE 6: Fix merge conflict

*Objective:* Update logger version and merge master into bugfix branch

bash
# 1. Switch to bugfix branch
git checkout bugfix/spelling-correction

# 2. Update logstash-logback-encoder to version 7.2 in build.gradle
# Edit build.gradle and change version to 7.2

# 3. Commit the change
git add build.gradle
git commit -m "Update logstash-logback-encoder to version 7.2"

# 4. Merge master into bugfix branch
git merge main

# 5. If there's a conflict, resolve it:
# - Open conflicted files
# - Remove conflict markers (<<<<<<, ======, >>>>>>)
# - Choose the correct version or combine both
# - Save files

# 6. Complete the merge
git add .
git commit -m "Resolve merge conflict between bugfix and main branches"


### EXERCISE 7: Revert commit

*Objective:* Fix spelling, update image, then revert image change

bash
# 1. Fix spelling mistake in index.html
# Edit src/main/webapp/index.html and fix spelling

# 2. Commit spelling fix
git add index.html
git commit -m "Fix spelling mistake in index.html"

# 3. Change image URL in separate commit
# Edit index.html and change image src

# 4. Commit image change
git add index.html
git commit -m "Update image URL in index.html"

# 5. Push both commits
git push

# 6. Revert the last commit (image change)
git revert HEAD
git push


### EXERCISE 8: Reset commit

*Objective:* Make local commit then reset it

bash
# 1. Update Bruno's role in appropriate file
# Edit the file and change Bruno's role to DevOps

# 2. Commit locally (don't push)
git add .
git commit -m "Update Bruno's role to DevOps team"

# 3. Reset the commit (since it's only local)
git reset HEAD~1
# or
git reset --soft HEAD~1  # keeps changes staged
git reset --hard HEAD~1  # discards changes completely


### EXERCISE 9: Merge

*Objective:* Merge bugfix branch into master using CLI

bash
# 1. Switch to main branch
git checkout main

# 2. Pull latest changes
git pull origin main

# 3. Merge bugfix branch
git merge bugfix/spelling-correction

# 4. Push merge commit
git push


### EXERCISE 10: Delete branches

*Objective:* Clean up local and remote branches

bash
# 1. Delete local branches
git branch -d feature/upgrade-dependencies
git branch -d bugfix/spelling-correction

# 2. Delete remote branches
git push origin --delete feature/upgrade-dependencies
git push origin --delete bugfix/spelling-correction

# 3. Verify branches are deleted
git branch -a


## Useful Git Commands Reference

bash
# Status and information
git status                    # Check repository status
git log --oneline            # View commit history
git branch -a                # List all branches
git remote -v                # Show remote repositories

# Working with branches
git checkout -b <branch-name> # Create and switch to new branch
git checkout <branch-name>    # Switch to existing branch
git branch <branch-name>      # Create branch without switching

# Staging and committing
git add .                     # Stage all changes
git add <file>               # Stage specific file
git commit -m "message"      # Commit with message
git commit --amend           # Modify last commit

# Remote operations
git push                     # Push to current branch
git push -u origin <branch>  # Push and set upstream
git pull                     # Pull latest changes
git fetch                    # Fetch without merging

# Merging and rebasing
git merge <branch>           # Merge branch into current
git rebase <branch>          # Rebase current branch onto another
git cherry-pick <commit>     # Apply specific commit

# Undoing changes
git reset HEAD~1             # Undo last commit (keep changes)
git reset --hard HEAD~1      # Undo last commit (discard changes)
git revert <commit>          # Create new commit that undoes previous
git checkout -- <file>      # Discard changes to file


## Tips for Suc…
