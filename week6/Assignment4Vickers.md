# Assignment #4 - Git Branching and Workflow

## Objective
This assignment focuses on working with branches and implementing a basic Git Flow workflow. The goal is to understand and practice branch management, feature development, and the pull request process.

## Activity 1: Working with Feature Branches

### Step 1: Create a Feature Branch in Visual Studio Code
First, I opened my project repository in Visual Studio Code and followed these steps:
1. Navigated to the Source Control view (three dots connected by lines icon)
2. Clicked on the current branch name at the bottom-left
3. Selected "+ Create new branch..." from the pop-up menu
4. Named the new branch "feature/assignment4"

[![Step 1: Creating a new branch](./SS1%20git%20branch.png)](./SS1%20git%20branch.png)

### Step 2: Verify Local and Remote Branches
To verify the branch creation and check the status of local and remote branches, I used the following commands:

```bash
git branch
```
This command showed my new branch with an asterisk (*) indicating it as the current working branch.

[![Step 2a: Local branches](./SS1%20git%20branch.png)](./SS1%20git%20branch.png)

```bash
git branch -r
```
This command showed only the remote main branch, as the feature branch hadn't been pushed yet.

[![Step 2b: Remote branches](./SS2%20git%20branch%20r.png)](./SS3%20Publish%20branch.png)

### Step 3: Commit Changes and Publish the Branch
After making changes to the README.md file:
1. Used the Source Control panel to stage changes
2. Added a descriptive commit message: "week 6 created"
3. Committed the changes
4. Published the branch to GitHub

[![Step 3: Committing and publishing changes](./SS3%20Publish%20branch.png)](./SS3%20Publish%20branch.png)

### Step 4: Create a Pull Request on GitHub
On GitHub:
1. Clicked the "Compare & pull request" button from the yellow notification bar
2. Set the base branch to main and compare branch to feature/assignment4
3. Added a title and description
4. Created the pull request
5. Merged the changes
6. Deleted the remote branch

#### Pull Request Process Screenshots:

1. Opening the Pull Request:
[![Step 4a: Opening pull request](./ss4%20git%20PR.png)](./ss4%20git%20PR.png)

2. Pull Request Created:
[![Step 4b: Pull request created](./SS5%20PR.png)](./SS5%20PR.png)

3. Pull Request Merged:
[![Step 4c: Pull request merged](./ss6%20PR%20created.png)](./ss6%20PR%20created.png)

4. Remote Branch Deleted:
[![Step 4d: Remote branch deleted](./SS7%20PR%20Deleted.png)](./SS7%20PR%20Deleted.png)

**Question: Will the local feature branch still exist?**
Yes, the local feature branch will still exist. Deleting the remote branch on GitHub only removes the branch from the remote repository and has no effect on the local branch on your computer.

### Step 5: Clean Up Local Repository
To clean up the local repository after merging:
1. Updated local metadata:
```bash
git fetch -p
```

2. Switched back to main branch:
```bash
git checkout main
```

3. Pulled the latest changes:
```bash
git pull
```

4. Deleted the local feature branch:
```bash
git branch -d feature/assignment4
```

[![Step 5: Branch cleanup completed](./SS8%20Branch%20Cleanup.png)](./SS8%20Branch%20Cleanup.png)
