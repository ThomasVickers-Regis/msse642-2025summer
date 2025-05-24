## ACTIVITY 1: Research git

<details>
        <summary><h2> Types of version control systems. What type is Git? </h2></summary>
        <p style="text-indent: 40px;"><b>Local Version Control Systems (LVCS)</b> are when the files for the project are stored on a single local device, and versions are controlled on a database on that machine. Developers pull the file and make modifications before storing them back on the device. This method can easily cause issues when more than one person is working on the same files because managing conflicting changes becomes difficult without a central point of coordination. All project history is stored locally, meaning loss of the local device can result in the loss of all version history. An example is the Revision Control System (RCS).</p>
        <img width="400" src="https://git-scm.com/book/en/v2/images/local.png"/>
        <br><br>
        <p style="text-indent: 40px;"><b>Centralized Version Control Systems (CVCS)</b> share a single repository on a server, and developers pull the files down from one central location. When they finish modifying the files, they push them back up to the same repository. Users typically "check out" files, which can sometimes lead to locking mechanisms to prevent conflicts, although this can restrict collaboration. Issues arise from this system when previous versions are lost on the central server or if the server goes offline; it becomes difficult to revert between changes or collaborate as all operations rely on the central server being available. Examples include Subversion (SVN) and Perforce.</p>
        <img width="400" src="https://git-scm.com/book/en/v2/images/centralized.png"/>
        <br><br>
        <p style="text-indent: 40px;"><b>Distributed Version Control Systems (DVCS)</b> are systems like Git. This system has a server and local machines where developers pull files from the server onto their local machine. Each local copy is a full-fledged repository with the complete project history. This allows the server to keep track of versions, and individual developers to track their changes locally, commit changes, and switch branches without needing a network connection. When they push back to the server, they can compare any conflicts in the data and merge. This allows for better version rollbacks and a better developer experience because developers have more control and flexibility with their local copies and have built-in backups of the entire project history. Git is the most widely used DVCS.</p>
        <img width="400" src="https://git-scm.com/book/en/v2/images/distributed.png"/>
        <br><br>
        <p>Reference:</p>
        <a href="https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control">https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control</a>
</details>

<details>
        <summary><h2> Snapshots</h2></summary>
        <p style="text-indent: 40px;">Git fundamentally thinks of its data as a series of <b>snapshots</b> to save states of files, rather than just tracking changes file by file. When you make a commit, Git basically takes a picture of what all your tracked files look like at that moment and stores a reference to that snapshot in the repository's object database. These states get stored in relation to concepts like the HEAD (a pointer to the current commit/branch), the Index (Staging Area), and the Working Directory. Most of the Git commands you are used to are basically checking the state of files in one of these areas compared to another (e.g., working directory vs. staging area, staging area vs. last commit), or by moving a snapshot from one state to another (e.g., from staging to a commit). While Git is efficient and can store data using deltas internally to save space (especially in packfiles), the core concept is based on saving the complete state (snapshot) of your project with each commit. For a greater breakdown of all the commands and how the snapshots and these areas work, check out the reference below.</p>
        <img width="400" src="https://git-scm.com/book/en/v2/images/reset-workflow.png"/>
        <br><br>
        <p>Reference:</p>
        <a href="https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified">https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified</a>
</details>

<details>
        <summary><h2> What is a repository? Remote vs. local. </h2></summary>
        <p style="text-indent: 40px;">A <b>repository</b> (or repo) is the central storage location for your project files and their entire history. It contains all the commits, branches, tags, and other information Git uses to manage your project versions. If you reference the diagram from the DVCS, you will see a remote repository is typically represented as the server, and the local repository is the one stored locally on your machine within a hidden <code>.git</code> directory. You can think of the remote as a cloud storage for project files that the team shares. The local is the version you pulled down to your machine that you work with, and where you can create instances of the files in your local Git's tracked states, as seen in the snapshots. Developers push their committed changes from their local repository to a remote repository and pull changes from a remote repository to update their local copy and collaborate, effectively synchronizing the repository history.</p>
</details>

<details>
        <summary><h2> What is working directory? </h2></summary>
        <p style="text-indent: 40px;">The <b>working directory</b> (or working tree) is the directory on your file system that contains the actual files you are currently working on. This is where you pulled all the files to your local machine. It's a single checkout of one version (commit) from the repository. You make edits, add new files, and delete files directly in the working directory. Your changes here are initially untracked or marked as "modified" by Git and will not affect any other developers' files directly in their working directories or the repository's history until you explicitly tell Git to notice them (usually by staging them in the Index tree).</p>
</details>

<details>
        <summary><h2> What is Staging Area </h2></summary>
        <p style="text-indent: 40px;">The <b>Staging Area</b> (also called the <b>Index</b> or Index Tree) is a crucial intermediate step between the working directory and the repository. It's a file, generally contained within the <code>.git</code> directory, that stores information about what will go into your next commit. You use the <code>git add</code> command to place specific changes or entire files from your working directory into the Staging Area. This allows you to carefully curate which specific modifications will be part of the upcoming snapshot, creating logical groups of changes for your commits. Some people use this as a temporary save state location in case they need to switch branches quickly without losing their current progress in the working directory. Staging is mostly used as a way to save your specific changes before they are fully ready for a more permanent save state with a commit. Changes in the working directory that have been added to the staging area are considered "staged changes".</p>
</details>

<details>
        <summary><h2> What is commit? </h2></summary>
        <p style="text-indent: 40px;">A <b>commit</b> is the operation of saving a snapshot of the changes currently in the <b>Staging Area</b> to your local Git repository's history. It's a key step in the DVCS workflow, creating a permanent point in the project's timeline. Each commit is an immutable object that saves information relating to the user who committed the files (author and committer), the date and time, a commit message describing the changes, and generates a unique identifier (a 40-character SHA-1 hash) that acts as a checksum and can be used to refer to this specific snapshot and roll back if needed. A commit also contains a pointer to the snapshot of the files it represents and pointers to its parent commit(s), forming the project's history as a Directed Acyclic Graph (DAG). The best way to use these, I have found, is to think of them as a save state in video games. You can go back to previous "games" (commits), but be mindful that rolling back in Git can involve complexities like potential data loss if not handled carefully, like losing the progression in a game if you load a pervious save. Once you are done with your edits and commits locally, you use <code>git push</code> to share these new commits with a remote repository, and its history updates.</p>
</details>

<details>
        <summary><h2> Find a good diagram that illustrates the architecture and the flow </h2></summary>
        <img width="500" src="https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fuser-images.githubusercontent.com%2F83613651%2F153767766-3c16ba10-75d2-4c28-8598-0163f8013965.png"/>
        <br><br>
        <p>Reference:</p>
        <a href="https://dev.to/vinothmohan/git-an-overview-at-high-level-2ckk">https://dev.to/vinothmohan/git-an-overview-at-high-level-2ckk</a>
</details>
