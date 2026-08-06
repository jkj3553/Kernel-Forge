# GIT - version control system
-  sources - [Boot.Dev](https://www.youtube.com/watch?v=rH3zE7VlIMs&t=6858s&pp=ygUPZ2l0aHViIHR1dG9yaWFs) , [FreeCodeCamp](https://www.youtube.com/watch?v=zTjRZNkhiEU)
 
#### Linus Torvalds created it in 5 days after one of the ymaintainer of Linux broke

---

- most of git commands are porcelain commands and rest are plumbing commands.
#### Repo:-
- repository is essentially a directory which contains a project (other directories and files)
- all of Git's internal tracking and versioning information is stored inside the hidden **.git** directory.
##### Status:-
 - A file can be in one of several states in a git repo. Here are few ones--
	 - Untracked - not being tracked by git
	 - Staged - marked for inclusion in the  next commit
	 - Committed - saved to  the repository's history
	   
- `git status` command shows you the current state of your repo
  
##### Staging:-
 - Staging is needed to track/stage a file before committing it later.
	 - `git add < path-to-file | pattern>`
	 - `git add .`  - stages all files in current directory and beyond, but not any directory above.
- `git restore <file>` - discard unstaged changes to a file.
- `git restore --staged <file>` - unstage a file without discarding changes

#### Commits:-
- `git commit` - opens editor(nano/vim or custom editor if set) to save/edit the commit message.
- `git commit -m "your commit message"` - to commit the staged files with a message.
- Commit is a snapshot of a repository at a given time.
- It saves the state of the repo and this is how git keeps tracks the changes in a file.
- git creates commit, which is a set of changes ties to an author, Date and other information.
- as many commits as you want can be added to the graph
- at any commit you can branch off and create new commits on the new line. Any of these branches can be merged at any point including the main line.
- More than once commits can be squashed into one commit.
- Commit messages can be edited
- Git commits can be reverted.
- `git commit --amend` - fix your last commit's message or add forgotten changes to it
- `git revert <commit_Hash>` - creates a new commit that undoes a previous one, safe for shared/public branches. This doesn't rewrite history.
- `git show <commit_Hash>` - view a specific commit's changes

#### **Git Log** -
- git repo is a list of commits where each commit represents the full state of the repository at  a given point in time.
-  the `git log` command  show a history of the commits in a repo.
- each commit has a unique identifier known as *commit hash*.
- git uses SHA-1 to generate commit hash.
- `git log --oneline` - clean list of commits


#### **Git reflog**(Very important safety-net/undo button):- 
- *stands for "reference log". It keeps a record of every place `HEAD` (and branch tips) has pointed to in your local repo — every commit, checkout, reset, rebase, merge, etc.*
- Unlike `git log`, which shows the commit history of your project, `reflog` shows the history of _your movements_ in that repo. It's local only — never pushed, never shared, never cloned by others.
- If you mess up with `git reset --hard`, delete a branch, or do a bad rebase and think you've "lost" commits — they're usually **not gone**. Git doesn't delete commit objects immediately; it just stops pointing to them. `reflog` still remembers where they were.
- `git reflog` — shows the list of recent HEAD movements, each with a short hash and a description of the action (commit, checkout, reset, rebase, etc.)
- `git reflog show <branch>` — shows reflog for a specific branch instead of HEAD.
- **Recovering lost work** — once you find the hash of the commit you want back (from reflog output):
	- `git reset --hard <hash>` — moves your branch back to that commit (careful, this discards current state)
	- `git checkout <hash>` — go look at that commit without changing your branch		- `git cherry-pick <hash>` — bring just that one commit's changes onto your current branch
	- `git branch recovered-branch <hash>` — safest option, creates a new branch pointing at the "lost" commit so nothing is at risk
#### Plumbing:-
-  all data in git repo is stored directly in the (hidden) .git directory. It includes all commits, branches, tags and other objects.
- Git is made up of Objects that are stored in the .git/objects directory.
- A commit is just a type of object. 
- git stores commits in format such that if commit hash is `39e33bcfb8cd5ae2d398d84f279013db5549a341`,  .git/objects will store such that inside directory `39` you will have The git commit object file named- `e33bcfb8cd5ae2d398d84f279013db5549a341`.
- This git commit object file has the contents compressed to raw bytes. That's why git commits remain small and light weight.
- **cat file (a plumbing command)** - 
	- `cat-file` is a git plumbing command allowing us to see the contents of a commit(or object file) without reading all that messy fuzz in object files directly.
	- syntax- `git cat-file -p <commit hash>`

#### Trees and Blobs:-
- **Tree** - git's way of storing a directory
- **Blob** - git's way of storing a file

#### Storing Data:-
- Git stores an entire snapshot of files on a per-commit level.  It does *NOT* store only the changes made in the commit.
- Git uses some performance optimizations so that your .git directory doesn't get too unbearably large.
	- it compresses and packs files to store them more effeciently
	- It de-duplicates files that are the same across different commits. If a file doesn't change between commits, Git will store it only once.

#### Config:-
- `git config --add --global user.name "TheJayTheKumar"`
- `git config --add --global user.email "jykr@email.com`
	- `git config` : Command to interact with git configuration
	- `--add`: Flag stating you want to add a configuration
	- `--global`: Flag stating you want this configuration to be stored globally in your `~./gitconfig`. The Opposite is "local" which stores the configuration in the current repository only.
	- `user`: The Section
	- `name`: The Key within the section
	- `"TheJayTheKumar"`: Value you want to set for the key.
- `git config --list --local/global`: to see all global/local key and values
-  `--list` gives us all the values, but `--get` gives us single value. For e.g. - `git config --get <key>`
-   **unset** : `git config --unset <key> <value>` , to remove a key value pair. 
	- `--unset-all`: to remove all occurences of key,value. 
- **Remove a Section** - `--remove-section` to remove an entire section from your Fit configuration. 

#### Branching:-
- A **Git Branch** allows you to keep track of different changes separately.
	- Eg.- let's say you have a big web project and you want to experiment with changing the color scheme. Instead of changing the entire project directly (as of right now, our master branch), you can create a new branch called `color_scheme` and work on that branch. When you're done, if you like the changes, you can *merge* the `color_scheme` branch back into the master branch to keep the changes. If you don't like the changes, you can simply delete the color_scheme branch and go back to the master branch. 
- Branch is just a pointer to a commit(latest commit), they're lightweight and "cheap" resource-wise to create. When you create 10 branches, you're not creating 10 copies of your project on your hard drive.
- GIT has its default branch as `master` but Github changed its default branch from `master` to `main`. Therefore it is important to change the default branch by using  `git branch -m oldbranch newbranch`.
- You can check your current branch by `git branch`
- You can **create a branch** by using two options--
	- `git branch my_new_branch` - creates a new branch but doesn't switch to it.
	- `git switch -c my_new_branch` - switch command allows you to switch branches and `-c` flag tells git to create a new branch if it doesn't exist.
- **Switching Branches** - `git switch branch_to_switch`
- **Log Flags**- to make `git log` outputs easier to read
	- `--decorate`
		- short(the default)
		- full(shows the full ref name)
		- no(no decoration)
	-  `--oneline` 
- **Changing branch name**- `git branch -M new_branch_name`

#### Merge:-
- After you create a branch, for let's say a feature you want to experiment with in your codebase, if you're happy with the changes and want it in your main codebase, you have to **merge**.
 - To merge a branch, `git merge branch_to_merge`,  you will have to create a **merge commit**.
 - Now when you command `git log --graph --oneline --parents`, you will see that this **merge commit**  will show to have two parents.
- **Fast Forward merge** - It is the simplest type of merge. When the branch has just one commit or that the base branch has **no new commit** and then that branch is to be merged. Then the pointer of the base branch is moved to the tip of the feature branch.
- **Delete a branch**- `git branch -d branch_to_delete`

#### Rebase:-
- Rebase means moving the merge base.
- It does not add an additional commit like Merge
- **When to Rebase?**
	- An advantage of merge is that it preserves the true history of the project. It shows when branches were merged and where. One disadvantage is that it can create a lot of merge commits, which can make the history harder to read and understand.
	- A linear history is generally easier to read, understand, and work with. Some teams enforce the usage of one or the other on their main branch, but generally speaking, you'll be able to do whatever you want with your own branches. 
	- **WARNING** 
		- You should never rebase a public branch (like` main`) onto anything else. Other developers have it checked out, and if you change its history, you'll cause a lot of problems for them. However, with your own branch, you can rebase onto other branches (including a public branch like main) as much as you want. 
		- NEVER Run rebase while you're on main/master branch.

#### Reset:-
 - Unlike revert, this rewrites history.
###### GIT Reset Soft--
 - used to undo the last commit(s) or any changes in the index(staged but not committed changes) and the worktree (unstaged and not committed changes).
	 - `git reset --soft COMMITHASH` 
	 - `--soft` is useful if you just want to go back to a previous commit but keep all your changes. Committed changes will be uncommitted and staged, while uncommitted changes will remain staged or unstaged as before.
##### GIT Reset Hard--
- used to go back to a previous commit and discard all the changes.
	- `git reset--hard COMMITHASH`

#### Remote:-
- They are just external repos with mostly the same Git history as our loacal repo.
- `git remote -v`- to check if a remote repo is set up(like github)
- `git remote add origin your_repo_URl` - connecting to a remote repo
- `git remote rename oldname newname` - changing remote repo name
- `git remote remove repo_name` - to remove connection to the remote repo

#### Git Diff-
- shows differences between the same file at x time vs that file at y time. It does not compare two different files.
- The newer file is represented by +++ while the older is represented by ---.
- `git diff --staged` - gives difference between all staged files and their unstaged versions

#### Git Stash-
- `git stash pop`
- stash is a temporary store of you made changes in a particular branch.
- you can change branches after making a change and not committing it, once you stash it.
- you can find your changes in another branch by using `git stash pop`.


### Github--
 - **Git is a version control command line tool for managing code files. GitHub is one of the services to host host your codebase managed by Git.**
 - You can connect your local git repo to your github using either SSH keys or HTTP Url. For SSH Keys generation and connection, refer - [Connect Git to GitHub Using SSH](https://decodementor.medium.com/connect-git-to-github-using-ssh-68ab338f4523)
#### Clone:-
- `git clone <repo_url>` - brings down the entire repo from remote repo to local repository on your system.

#### Push:-
- `git push -u origin main` - pushing main branch to origin remote repo and `-u` sets up origin as the upstream for main branch. After this you can just run `git push` on main branch
- **upstream**- linking origin to the main.

#### Pull and Fetch:- 
- `git fetch`- gets info but doesn't put in my working area.
- `git pull` - gets info and adds it in my working area
- ![[Pasted image 20260806095215.png]]


#### Open-Source(Github)--

- **Fork** - a copy of a repository.
	- Forking allows you to freely experiment with changes without affecting original project.
- Always create a separate branch for your contribution and not in the `main` branch
- To push your changed code and commit to the repo of only your working branch -- `git push origin your_branch_name` 
- **Compare & Pull Request** - Sending your changed codebase to the maintainer/owner of the open-souce repo.
	- **Be very cautious and thoughtful** about the pull request's *title* and *description*
	- Write neat and detailed description of the Pull Request.
 