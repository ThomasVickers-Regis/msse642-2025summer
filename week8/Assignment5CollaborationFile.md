# Assignment 5 Collaboration File

## Team C Collaboration Instructions

**Team Members:**
- Spencer
- Ben  
- Thomas (Repository Owner)
- Nigel

This file is designed for team collaboration using Git workflow. Each team member will follow these steps to contribute to their teammates' repositories.

---

## Step 1: Create Your Own Collaboration File

**Action**: Create a new file in your repository called "Assignment5CollaborationFile.md"

**Instructions**:
1. In your local repository, create a new file named `Assignment5CollaborationFile.md`
2. Add a basic header and description (like this file)
3. Commit and push this file to your main branch
4. Share your repository URL with your team members

- **Thomas**: https://github.com/ThomasVickers-Regis/msse642-2025summer.git

---

## Step 2: Clone Your Teammates' Repositories

**Action**: Each member will clone the repositories of other team members

**Instructions**:
1. Get the repository URLs from your teammates (see above)
2. Open your terminal/command prompt
3. Navigate to a directory where you want to store the cloned repositories
4. Run the clone command for each teammate's repository:
   ```bash
   git clone [teammate-repository-url]
   ```
5. Verify the clone was successful by checking the directory contents

**Example for Team C**:
```bash
git clone https://github.com/ThomasVickers-Regis/msse642-2025summer.git
git clone [Spencer's-repo-url]
git clone [Ben's-repo-url]
git clone [Nigel's-repo-url]
```

---

## Step 3: Create a Local Branch with Your Name

**Action**: Make a local branch that is named with your name

**Instructions**:
1. Navigate into the cloned repository directory
2. Check the current branch: `git branch`
3. Create and switch to a new branch with your name:
   ```bash
   git checkout -b [your-name]
   ```
4. Verify you're on the new branch: `git branch`

**Example for Team C**:
```bash
cd msse642-2025summer
git checkout -b spencer
# or
git checkout -b ben
# or
git checkout -b nigel
```

---

## Step 3.5: Update Remote URL (If Needed)

**Action**: Update the remote URL to point to your fork if you don't have write access

**Instructions**:
1. After cloning, check your remote configuration:
   ```bash
   git remote -v
   ```
2. If you get permission errors when pushing, you need to update remote to your fork:
   - Update the remote to point to your fork:
   ```bash
   git remote set-url origin https://github.com/[your-username]/[repository-name].git
   ```
3. Verify the remote is updated:
   ```bash
   git remote -v
   ```

**Example**:
```bash
# If you cloned Ben's repo but don't have write access
git remote set-url origin https://github.com/ThomasVickers-Regis/msse642.git
```
```bash
git remote -v
#should show your forks address as the remote address
origin  https://github.com/ThomasVickers-Regis/msse642.git (fetch)
origin  https://github.com/ThomasVickers-Regis/msse642.git (push)
```

---

## Step 4: Make Changes, Commit, and Publish the Branch

**Action**: Make changes to the file, commit, and publish the branch

**Instructions**:
1. Open the `Assignment5CollaborationFile.md` file
2. Add your name and a brief message to the file (see format below)
3. Save the file
4. Stage your changes: `git add Assignment5CollaborationFile.md`
5. Commit your changes with a descriptive message:
   ```bash
   git commit -m "Add [your-name] to collaboration file"
   ```
6. Push your branch to the remote repository:
   ```bash
   git push origin [your-branch-name]
   ```

**Example File Addition**:
```markdown
## Team Members Who Have Contributed

- **Thomas Vickers** - Repository owner
- **Spencer** - Added on [date]
- **Ben** - Added on [date]
- **Nigel** - Added on [date]
```

---

## Step 5: Submit a Pull Request

**Action**: Submit a pull request to merge your branch

**Instructions**:
1. Go to the repository on GitHub/GitLab
2. You should see a notification about your recently pushed branch
3. Click "Compare & pull request" or "Create pull request"
4. Fill in the pull request details:
   - **Title**: "Add [your-name] to collaboration file"
   - **Description**: Brief description of your changes
5. Click "Create pull request"

**Example Pull Request for Team C**:
- **Title**: "Add Spencer to collaboration file"
- **Description**: "Added my name to the team members list in the collaboration file as part of Assignment 5."

## Screenshot

### PR created on forked branch
![Ben PR Header](./SS1%20Ben%20PR%20Header.png)

### PR submitted to teammate's repository
![PR created Ben](./SS2%20PR%20created%20Ben.png)

---

## Step 6: Review and Merge Pull Requests

**Action**: The owner of the repo accepts or rejects the pull request

**Instructions** (for repository owners):
1. Go to the "Pull requests" tab in your repository
2. Review each pull request:
   - Check the changes made
   - Ensure the branch name follows the naming convention
   - Verify the commit message is descriptive
3. If the changes look good:
   - Click "Merge pull request"
   - Confirm the merge
   - Delete the branch (optional)
4. If changes are needed:
   - Add comments requesting modifications
   - Wait for the contributor to update the PR

---

## Team Members Who Have Contributed

*This section will be populated as team members complete their contributions*

- **Thomas Vickers** - Repository owner

