## Cases:
	- ### Case 1: Start from an existing remote repository (use `clone`)
	  collapsed:: true
		- Suppose GitHub already has a repository.
		  
		  ```bash
		  git clone https://github.com/user/repo.git
		  cd repo
		  git checkout -b java origin/java  # git checkout -> Switches to a branch.
		  # -b java -> Creates a new local branch named java.
		  # Uses the remote branch origin/java as the starting point for the new local branch.
		  ```
		  
		  Notice there is **no `git init`**.
		  
		  Why? Because `git clone` already:
			- Creates the folder.
			- Creates the `.git` directory.
			- Downloads the complete commit history.
			- Sets up `origin`.
			- Checks out the default branch (`main`).
			  Running `git init` before `git clone` would be unnecessary.
	- ### Case 2: Merging a Local  existing Git Repository with an Existing Remote Repository
	  collapsed:: true
		- ```bash
		  git init
		  git add .
		  git commit -m "Initial local commit"
		  
		  git remote add origin https://github.com/Android5551/Java.git # Git only knows the URL
		  # —it doesn't automatically know the remote branches.
		  
		  git fetch origin
		  git branch -r
		  git branch
		  git branch -M main //-M means rename the current branch.
		  
		  git merge origin/main --allow-unrelated-histories
		  
		  # resolve conflicts if needed
		  
		  git push origin main
		  ```
			- #### rename the current branch
				- `git branch -M main` renames the existing branch to main
			- #### delete the said branch
				- `git branch -d main` deletes the main branch
			- #### fetch the remote repo info
				- `git fetch origin`
				- >**Contact the remote repository named `origin` and download its latest commits, branches, and tags, but do not change my current working branch.**
				- Think of it as **"download updates without applying them.**
			- #### Remote tracking branches
				- `git branch -r`
					- Show remote-tracking branches that your local Git knows about.
			- #### see which local branches track which remote branches
				- ```
				  git branch -vv
				  ```
				- `git branch` → list branches
				- first `-v` → show the latest commit information
				- second `-v` → show tracking information (remote branch)
	- ### Case 2-1: when current branch in local are not same as branches in remote
	  collapsed:: true
		- ```bash
		  # first commit the changes in existing branch and push to cuuurent branch in remote
		  git add .  
		  git commit -m "ok"
		  git push origin java         # upload java branch to remote
		  
		  #  fetch the updates, commits etc from remote but not download it to cuurent
		  git fetch origin
		  git branch -r     # show remote branches
		  
		  git checkout -b main origin/main # create local main from remote main
		  
		  git branch -vv # show branches + tracking info
		  ```
	- ### Case 3: Local repository has commits, remote repository is empty
	  collapsed:: true
		- ### Initialize Git
		  collapsed:: true
			- ```
			  git init
			  ```
		- ### Check what is changed
		  collapsed:: true
			- ```
			  git status
			  ```
		- ### Stage files
		  collapsed:: true
			- ```
			  git add .
			  ```
		- ### Commit
		  collapsed:: true
			- ```
			  git commit -m "Initial commit"
			  ```
		- ### Create a remote repo
		  collapsed:: true
			- #### Connect local repo to Github
				- ```
				  git remote add origin https://github.com/yourusername/java.git
				  ```
			- #### If branch is main and if this is the first push to a branch
				- ```
				  git push -u origin main
				  /* The -u option tells Git to remember that
				  your local main branch tracks origin/main. 
				  After /that, future pushes can usually be just:
				  git push
				  */
				  ```
			- #### If not:
				- ##### Create and switch to the java branch:
					- ```
					  git checkout -b java
					  ```
				- ##### If java branch already exists on Github
					- Simply switch to it locally and pull it first if needed:
						- ```
						  git checkout java
						  ```
					- push
						- ```
						  git push origin java
						  ```
		- ### connect your GitHub repository:
		  collapsed:: true
			- ```
			  git remote add origin https://github.com/yourusername/CoreJava.git
			  ```
		- ### Push the java branch:
		  collapsed:: true
			- ```
			  git push -u origin java
			  ```
	- ### Case 4: Pulling from git-hub to local repo
	  collapsed:: true
		- #### Git Stash, Pull, and Restore Workflow
			- This workflow is useful when you have **uncommitted changes** but want to update your local branch with the latest changes from the remote repository.
		- #### 1. `git stash`
		  collapsed:: true
			- **Purpose**
				- Temporarily saves your uncommitted changes (both staged and un-staged) and restores your working directory to the last commit.
				- It is useful when:
					- You need to pull the latest changes.
					- You want to switch branches.
					- You don't want to create a temporary commit
						- ```bash
						  git stash
						  ```
				- ##### What happens?
					- Before:
					  
					  ```
					  Working Directory
					  ├── pages/git.md (modified)
					  └── other files
					  ```
					  
					  After:
					  
					  ```
					  Working Directory
					  ├── Clean (no local changes)
					  
					  Stash
					  └── Saved copy of pages/git.md changes
					  ```
					  
					  Your changes are **not deleted**. They are stored in Git's stash.
		- #### 2. `git pull origin main`
		  collapsed:: true
			- ##### Purpose
				- Downloads the latest commits from the `main` branch of the `origin` remote and merges them into your current branch.
			- ##### Command
				- ```bash
				  git pull origin main
				  ```
			- This command performs two operations:
			  collapsed:: true
				- 1. **Fetch**
					- Downloads the latest commits from GitHub.
				- 2. **Merge**
					- Merges those commits into your local branch.
					  Equivalent to:
						- ```bash
						  git fetch origin
						  git merge origin/main
						  ```
		- #### 3. `git stash pop`
			- ##### Purpose
			  collapsed:: true
				- Restores the most recently stashed changes and removes them from the stash list.
			- ##### Command
				- ```bash
				  git stash pop
				  ```
			- ##### What happens?
				- Before:
				  
				  ```
				  Working Directory
				  └── Clean
				  
				  Stash
				  └── Your saved changes
				  ```
				  
				  After:
				  
				  ```
				  Working Directory
				  └── Your changes restored
				  
				  Stash
				  └── Empty (latest stash removed)
				  ```
		- #### Why use this workflow?
		  
		  Without stashing:
		  
		  ```
		  Local Changes
		      +
		  git pull
		      ↓
		  Possible merge conflict or Git refuses to merge
		  ```
		  
		  With stashing:
		  
		  ```
		  Local Changes
		      ↓
		  git stash
		      ↓
		  Clean Working Directory
		      ↓
		  git pull origin main
		      ↓
		  Updated Local Branch
		      ↓
		  git stash pop
		      ↓
		  Continue Working
		  ```
		  
		  ---
		- This workflow helps avoid conflicts when pulling with unfinished work.
	- ### Case 5: When the remote contains work that you do not have locally
	  collapsed:: true
		- ```bash
		  # Rebase is currently paused because Git found conflicts.
		  # This command removes the Eclipse workspace metadata folder (.metadata)
		  # from Git tracking to resolve the modify/delete conflicts.
		  git rm -r .metadata
		  
		  
		  # Stage the resolved changes.
		  # "git add" tells Git: I have fixed the conflicts, use these changes.
		  git add .
		  
		  
		  # Continue the paused rebase.
		  # Rebase means Git is taking your local commits and replaying them
		  # on top of the latest commits from the remote branch (origin/java).
		  # This keeps history clean instead of creating an extra merge commit.
		  git rebase --continue
		  
		  
		  # Check whether the rebase finished successfully
		  # and see the current state of your branch.
		  git status
		  
		  
		  # Create or open the .gitignore file.
		  # .gitignore tells Git which files/folders should NOT be tracked.
		  notepad .gitignore
		  
		  
		  # Add this line inside .gitignore:
		  # This prevents Eclipse workspace files from being added to Git again.
		  .metadata/
		  
		  
		  # Add the .gitignore changes to Git staging.
		  git add .gitignore
		  
		  
		  # Save the .gitignore change as a new commit.
		  # This commit permanently tells Git to ignore Eclipse metadata files.
		  git commit -m "Ignore Eclipse metadata"
		  
		  
		  # Upload your local java branch to GitHub.
		  # The rebase is complete, so the push should now be accepted.
		  git push origin java
		  ```
- ## Habbit for existing
  collapsed:: true
	- ### Start of the day ("Check Out")
		- Switch to the branch you'll work on:
		- #+BEGIN_TIP
		  before checkout commit your changes
		  #+END_TIP
		- ```
		  git switch main or git checkout main
		  
		  ```
		  
		  or
		  
		  ```
		  git switch feature-xyz
		  ```
		- Update it:
			- ```
			  git pull origin main
			  ```
			  (or `git pull origin feature-xyz`)
			  Now you're working on the latest code.
	- ### End of the day ("Check In")
	  collapsed:: true
		- ```
		  git add .
		  git commit -m "Completed login validation"
		  git push origin main (if set upstream like git push -u origin main so only git push suffice)
		  ```
		  
		  or, if you're on a feature branch:
		  
		  ```
		  git push origin feature-xyz
		  ```
		  
		  This ensures your work is saved on the remote repository.
- ---
- [[Thu, 09.07.2026]]
  collapsed:: true
	- `git init`
		- initialize git
		- creates .git folder
	- `git clone  url`
		- creates remote repo copy to local repo
		- creates project folder and readme file
	- make folder, make changes
	- Open CMD wherever `readme.md` file is present
	- `git add .`
		- The files you need to send to github is prepared or checked or tracked here like updated files, made changes etc.
		- `.` -> current folder
	- `git commit -am "message"`
		- commit changes done in `.git` or local repo
	- `git push`
		- reflects or final commit the changes in global repo
	- #+BEGIN_NOTE
	  What if we don't put `git add .` instead we used `git commit -am "message`
	  + new files won't show/track if you added them; it will be there on local machine as it is but if you had modified old files it will show/track them.
	  #+END_NOTE
	- > if you want commit only one file then use
	  > + `git add filename.txt`
	- > Once you have committed don't clone again it will create project from scratch
	  > + Instead use `git pull`
		- `git pull`
			- When everyone committed their commits on git ; git repo has all the common codes from different people ; to track all the changes done by all you use `git pull` in same folder on **main branch**
			- to track new changes in  your own repo
			- the people which made changes in main repo reflects in local repo
	- ### To add members or making team using gitusername
		- `Settings` -> `Collaborators`
			- Accept request on your mail
	- > Developers won't commit directly on main branch
		- Instead create branches
			- Open cmd from readme.md file
			- `git checkout -b branch-name`
				- creates new branch
			- `git checkout branch-name`
				- if 2-3 branches are there, need to switch to another use this command
				- deletes the branch once you checkout and switch to another in local machine
				  it will show  only code that belongs to that branch
			- so now the code will be on your branch until and unless team lead merges to main or pull to main
			- now `git add .`, `git commit`
				- `git push` -> final commits to main branch but this is other branch
					- ### Checkout (going from workspace)
					- `git push origin branch-name`
						- code commits to your branch
						- It is called checkout
						-
	- ### Merge code of other branch in main branch
		- Go to other branch > Contribute > open  pull request > create pull request > merge pull request > confirm merge
			- can delete branches too
	- ### Checkin (going to workspace)
		- next day you want updated code
		- You don't use `git clone`
		- if only main branch
			- then `git pull` ; all changes made on main reflects on local machine
		- else as it has other branches too; so git got confused which one to pull
			- `git pull origin main`
			-
	-
		- ### Simple comparison 
		  
		  | Old term | Git command | Meaning |
		  | ---- | ---- | ---- |
		  | Check out | `git checkout java` | Get/switch to a branch |
		  | Check in | `git add` + `git commit` + `git push` | Save and upload changes |
		  
		  ---
		  
		  Think of it like this:
		  
		  ```
		  GitHub
		  |
		  | git pull
		  ↓
		  Your local repository
		  |
		  | git checkout java
		  ↓
		  Work on java branch
		  |
		  | git add + git commit
		  ↓
		  Saved locally
		  |
		  | git push
		  ↓
		  GitHub
		  ```
		  
		  So:
		- **Checkout = "I want to work on this branch"**
		- **Check-in = "I finished my work and want to save/share it"**
		-
		-
		-