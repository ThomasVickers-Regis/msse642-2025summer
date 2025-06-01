# Assignment #3: Git Command Line Basics

## Configuration

### 1. What are the commands to configure your user.name and your user.email? Should this be configured globally or in your repo? Why or why not?
```bash
# Global configuration
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Local configuration (for specific repo)
git config user.name "Your Name (for this repo)"
git config user.email "your.repo.email@example.com"
```

Configuring global or local depends if you work on more than one project on your computer. If you use your computer for only your projects then global is a good way to add your account to all of your projects. If you work with other organizations or with other accounts and need to switch its better to set them locally for each repo/branch.

![Git config](./SS1%20gitconfig.png)
![Git config](./SS1%20gitconfig2.png)

### 2. How do you configure the core editor for git?
```bash
git config --global core.editor "code --wait"
```

### 3. How do you view your global config and your local (for the repo) config?
```bash
# View global config
git config --global --list

# View local config
git config --local --list
```

## Working with a Local Repo

### 4. What are the steps to create a new local repo via the CLI?
```bash
# Create and navigate to directory
mkdir my-new-repo
cd my-new-repo

# Initialize repository
git init
```

![Git init](./SS3%20git%20init.png)

### 5. How do you clone a repo and what's the difference between cloning and creating a new repo from scratch? Practice cloning a public repo from somewhere.
```bash
git clone https://github.com/octocat/Spoon-Knife.git
```

Git init is used on a blank project to get it ready to push up to github. Git clone is used to pull down existing repos onto your machine.

![Git Clone](../week3/SS4%20-%20VSC%20class%20workstation.png)

### 6. How do you look at the status of your repo? What information does this give you?
```bash
git status
```

Git status shows you the branch you are on and any staged or unstaged changes on that working branch.

![Git status](./SS%20git%20status.png)

### 7. How do you stage changes to your local repo in preparation for a commit?
```bash
# Stage specific file
git add my_file.txt

# Stage all changes
git add .

# Stage modified files only
git add -u
```

### 8. How do you commit changes to your local repo?
```bash
git commit -m "Your descriptive commit message here"
```

![git remote](./git%20add.png)

### 9. Include an example of a file that will allow you to "ignore" files in your repo. What kinds of files should not be part of your version control?
```gitignore
# Log files
*.log
logs/

# Operating System files
.DS_Store
Thumbs.db

# Build artifacts
/build/
/dist/
*.o
*.pyc
*.class

# Dependency directories
node_modules/
vendor/

# Environment variables
.env
.env.local

# IDE and editor files
.vscode/
.idea/
*.swp
```

Any file that contains sensitive data relating API keys, database credentials, or secrets. Generated files, dependency directories, or user specific files.

### 10. When files are under version control, you can't delete them using the OS commands. How do you delete files using git?
```bash
# Delete file and stage deletion
git rm filename.txt

# Remove from Git but keep locally
git rm --cached sensitive_data.txt
```

## Working with a Remote

### 11. How do you view the remote repo that is associated with your local repo?
```bash
git remote -v
```

![git remote](./SS%20git%20remote.png)

### 12. What is the function of the git fetch command?
```bash
git fetch origin
```
![git remote](./git%20fetch.png)

Git fetch is used to pull down changes made by other users without merging them into your local branch.

### 13. What is the difference between fetch and pull? Practice using both and show the results.
```bash
# Fetch
git fetch origin

# Pull
git pull origin main
```

Git pull does what fetch does but then also merges those changes into your local branch. If there is any conflicts it will highlight them and allow you to resolve any conflicts before finishing the merge.

### 14. Make some changes in your repo and using the command line to sync those changes with your remote repo. Show the results.
```bash
# Stage changes
git add .

# Commit changes
git commit -m "Your commit message"

# Push to remote
git push origin main
```

![git remote](./git%20add.png)

## Branches

### 15. How do you view the local and the remote branches for your repositories?
```bash
# View local branches
git branch

# View all branches (local and remote)
git branch -a
```

![git remote](./git%20branch.png)

### 16. View the local branches and create a new branch. Look again. Show before and after.
```bash
# View branches before
git branch

# Create new branch
git branch feature/user-profile

# View branches after
git branch
```

![git remote](./git%20branch2.png)

### 17. What are different ways to switch to a new branch?
```bash
# Method 1: Using switch
git switch feature/user-profile

# Method 2: Using checkout
git checkout feature/user-profile

# Method 3: Create and switch in one command
git switch -c another-new-branch
# OR
git checkout -b another-new-branch
```

### 18. Delete your local branch without pushing to a remote or merging to your main branch. Show that it's gone.
```bash
# Delete branch
git branch -D feature/user-profile

# Verify branch is gone
git branch
```

![git remote](./git%20branch3.png)
