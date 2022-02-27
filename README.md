# Git and Command Line 💻

🚀 Git Commands on a daily basis (maybe?) 🚀

## Table of Contents

- [Bash shortcuts for Maximum Productivity](#bash-shortcuts-for-maximum-productivity)
- [Understanding the Github flow](#understanding-the-github-flow)
- [Git workflow in real world projects (Branching workflow)](#git-workflow-in-real-world-projects-branching-workflow)

---

- [Initialize a git folder in a local repository](#initialize-a-git-folder-in-a-local-repository)
- [Check working status](#check-working-status)
- [Add files to staging area](#add-files-to-staging-area)
- [Remove a file from staging area, unstage](#remove-a-file-from-staging-area-unstage)
  - [Git: Should merged branch be always deleted?](#git-should-merged-branch-be-always-deleted)
  - [Git Tutorial: Fixing Common Mistakes and Undoing Bad Commits](#git-tutorial-fixing-common-mistakes-and-undoing-bad-commits)
- [Commit files](#commit-files)
- [Add a repository being a remote repository](#add-a-repository-being-a-remote-repository)
  - [Git error - Fatal: remote origin already exists and how to fix it](#git-error-fatal-remote-origin-already-exists-and-how-to-fix-it)
  - [How to check the remote origin URL of a local Git repository](#how-to-check-the-remote-origin-url-of-a-local-git-repository)
- [List all the repositories](#list-all-the-repositories)
- [Push code to a remote repository](#push-code-to-a-remote-repository)
- [Clone the project from remote repository to local](#clone-the-project-from-remote-repository-to-local)
- [Pull code from remote repository](#pull-code-from-remote-repository)
- [Rename files and folders](#rename-files-and-folders)
- [Branching and Merging](#branching-and-merging)
- [Stashing and Cleaning](#stashing-and-cleaning)
- [See commits and history](#see-commits-and-history)
- [Alias](#alias)
- [Squashing: combining multiple commits into one, for a cleaner git history](#squashing-combining-multiple-commits-into-one-for-a-cleaner-git-history)
- [Rebase](#rebase)

## Bash Shortcuts For Maximum Productivity

https://skorks.com/2009/09/bash-shortcuts-for-maximum-productivity/

I've listed a few useful shortcuts:

- `Ctrl + a` go to the start of the command line
- `Ctrl + e` go to the end of the command line
- `Ctrl + u` Delete left of the cursor
- `Ctrl + k` Delete right of the cursor
- `Ctrl + w` Delete word on the left (the same as Ctrl + backspace)
- `Alt + Enter` Toggle full screen mode

```bash
cd /d/Studying/Programming/git-practice
cd /d/Studying/Programming/git-practice
cd D:\Studying\Programming\react-projects-doing-for-learning\
```

## Understanding the Github flow

https://guides.github.com/introduction/flow/

## Git workflow in real world projects (Branching workflow)

- Create a new branch in local.
- Work on that branch in local, and commit changes in local.
- Push that code in remote repo (Github, etc).
- Create pull request (merge request from new branch to `main` remote repository).
- Merge code from that branch to main/dev branch in remote repo (somebody _might_ check before merging code, leave comment, etc). After that if everything works fine, merge that branch to main branch on remote repo.
- Pull code from remote to local.

- Example commands

```bash
git branch feature/login          # when in local
git add .
git commit -m 'Add login feature'
git push origin feature/login
git switch dev                    # or main branch
git pull origin dev
```

https://wildlyinaccurate.com/a-hackers-guide-to-git/

- About HEAD pointer: The way git knows which branch we're on is a special pointer called HEAD. HEAD is a pointer that normally points to a branch. Since HEAD usually points to a branch and not directly to a commit, it is sometimes called a symbolic pointer.

- Git & GitHub Crash Course For Beginners
  https://www.youtube.com/watch?v=SWYqp7iY_Tc

```bash
ls                    # list all files
dir                   # list all folders
touch index.html      # create a file
rm index.html         # remove a file
mkdir newfolder       # create a folder
rmdir newfolder       # remove a folder
```

- Check git version

```bash
git --version
```

## Config local user

```bash
git config --global user.name 'Your Name'
git config --global user.email 'example@gmail.com'
```

```bash
git config --list
git config --help
git help config
```

- **From Programming with Mosh Git course:** All these configuration settings are stored in a text file, we can edit that file using our default editor, this case VS code. Without this config above, we normally use Vim terminal to edit these configuration. git config --global -e.

```bash
git config global core.editor 'code --wait'
```

- For Windows

```bash
git config --global core.autocrlf true
```

- For macOS

```bash
git config --global core.autocrlf input
```

## Initialize a .git folder in a local repository

```bash
git init
rm -rf .git     # remove .git folder
```

## Check working status

```bash
git status
git status -s   # s for short
```

https://git-scm.com/docs/git-status

```bash
git diff --staged       # show difference between staging area and our most recent commit.
git diff main..develop  # show difference between 'main' and 'develop' branch our most recent commit
```

## Add files to staging area

```bash
git add *.html    # add all .html files
git add *.js      # add all .js files
git add .         # add all files that have been changed
git add -A        # add all files that have been changed
```

## Remove a file from staging area, unstage

```bash
git rm --cached index.html
git rm --cached .
```

## Commit files

```bash
git commit -m 'Comment here'
git commit -a -m 'Comment here'   # add files to staging area and commit simultaneously
```

In order to get out of **Insert Mode** (if you type `git commit` command and no `-m` after.): Esc and type `:wq`

### Git: should merged branch be always deleted?

https://stackoverflow.com/questions/15762183/git-should-merged-branch-be-always-deleted

- One of the comment: "Where I work, we use this as our workflow model. When we implement a change we create a feature branch and put in an empty commit to describe the branch."

```bash
git checkout -b feature1
git commit --allow-empty -m "Create branch to add a menu."
```

- "When we're done with this work, or hit a good stopping point, we merge in the feature branch (non-fast-forward) and delete the feature branch."

```bash
git checkout develop
git merge --no-ff feature1
git branch -d feature1
```

- "The branch history is still retained as a "lane change" under git. This allows us good visibility in what was changed for that feature, but avoids cluttering up the list of branches we have."

### Git Tutorial: Fixing Common Mistakes and Undoing Bad Commits

https://www.youtube.com/watch?v=FdZecVxzJbk

- Change the last commit, also change the history (because the hash key changes)

```bash
git commit --amend -m 'Change comment of the last commit'
```

- [7:06] shows the files that were changed within the commit

```bash
git log --stat
```

- When we want to move the commits from main (wrong commit) to a different branch (feature/subtract-function), we use `git cherry-pick`

```bash
git cherry-pick 0e5e78z
```

- Case: In main branch, we have 2 commits, using git log we can see them.

```bash
git log
commit 1b818d3...
Author:...
Date:...
Completed Subtract Function
commit 2e75207...
Author:...
Date:...
Initial commit
```

- But we realize the latest commit is not meant to be in master branch. We want to move the last commit to `feature/subtract-function`

```bash
git log
git switch feature/subtract-function
git cherry-pick 1b818d3     # copy the hash of the last commit, in this case 1b818d3
```

- If we want to delete the last commit in main after moving that commit to `feature/subtract-function`, use `git reset`
- 3 different types of reset:

  - [10:58] `git reset soft`
    It will reset us back to the commit we specifed but it will keep our changes that we've made in the staging area (green text)

    ```bash
    git reset --soft 2e75207
    ```

  - [11:38] `git reset mixed` (default)
    It will reset us back to the commit we specifed but it will keep our changes that we've made NOT in the staging area but in the working area (red text)

    ```bash
    git reset 2e75207
    ```

  - [12:30] `git reset hard`
    It reverts all of the tracked files back to the state they were but it leaves any untracked files alone. We still have some leftovers with git reset hard. We can use git clean to get rid of untracked files.

    ```bash
      git reset --hard 2e75207
    ```

- [13:40]

  ```bash
  git clean -df    # -d: untracked directories, -f: untracked files
  ```

- **My own notes**: If you want the same function in VS Code (Source Control when Ctrl + B), use `git reset hard --HEAD`

- [15:01] `git reflog`

- [18:10] we shouldn't change the git history if other people have pulled those changes already. In a situation where you really need to undo some commits but other people have aleady pulled those changes. In a situation like that, you're gonna want to use git revert. Revert creates new commits to reverse the effect of some earlier commits, so this way we don't rewrite any history.

## Add a repository being a remote repository

`git remote add [name] [link]`

```bash
git remote add origin https://github.com/nguyenhieptech/devc-2020
```

### Git error Fatal: remote origin already exists and how to fix it

https://www.datree.io/resources/git-error-fatal-remote-origin-already-exists

```bash
git remote set-url origin https://github.com/username/repository
```

### How to check the remote origin URL of a local Git repository?

https://www.digitalocean.com/community/questions/how-to-check-the-remote-origin-url-of-a-local-git-repository

```bash
git config --get remote.origin.url
git remote -v
git remote show origin
```

## List all the repositories

```bash
git remote
```

## Push code to a remote repository

`git push origin [branch_name]`

```bash
git push origin main
git push -u origin main       # u: coordinates the two branches (local and on server)
git push -u origin develop
```

## Clone the project from remote repository to local

`git clone [url]`

```bash
git clone https://github.com/username/repo-name
```

## Pull code from remote repository

`git pull origin [branch_name]`

```bash
git pull origin main
git pull origin dev
git pull origin feature/one
```

## Rename files and folders

- https://makolyte.com/how-to-change-the-casing-of-a-filename-when-using-git-on-windows/

- When you rename a file by changing its casing on Windows (ex: movie.cs -> Movie.cs), git will ignore the change. This behavior is controlled by the git core.ignorecase setting, which is true by default (at least on Windows). This is why it ignores filename casing changes.
- https://stackoverflow.com/questions/60970855/git-folder-name-change-locally-not-pushing-to-remote

- Rename files

```bash
git mv Colors.js colors.js
```

- Rename folders

```bash
git mv Services temp    # we need to do it in 2 steps
git mv temp services
```

## Branching and Merging

https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging

- List all branches
  git branch -a : also list all branches in remote repo (GitHub for example)

```bash
git branch
git branch -a   # also list all branches in remote repo (GitHub for example)
```

- Create a new branch `git branch [branch_name]`

```bash
git branch feature/main-layout
git branch feature/authentication
git branch bugfix/one
```

- Delete a branch in the remote repository

```bash
git push origin --delete feature/login
```

- Shorthand for create a new branch and switch to that new branch

```bash
git switch -b feature/signup
git checkout -b feature/signup
```

- Delete a branch

```bash
git branch -d feature/signup    # only work when we've merged the branch
git branch -D feature/signup    # delete the branch without needing to merge
```

- Change between branches
  git switch [branch_name]

```bash
git switch main
git switch feature/login  # or git checkout feature/login
git checkout -            # go to previous branch that you were working on
```

- `main` branch is going to be received code from `hotfix` branch.

```bash
git switch main
git merge hotfix
```

## Stashing and Cleaning

https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning

- Temporarily shelves (or stashes) changes you've made to your working copy so you can work on something else, and then come back and re-apply them later on. Stashing is handy if you need to quickly switch context and work on something else, but you're mid-way through a code change and aren't quite ready to commit.

https://bluecast.tech/blog/git-stash/

- `git stash save` is deprecated in favour of git stash push (https://www.git-scm.com/docs/git-stash)

- Basic commands

```bash
git stash
git stash -m 'comment'        # add comment to be more specific
git stash push -m 'comment'
```

- See which stashes you’ve stored

```bash
git stash list
```

- Apply a stash and keep the stash. You can use the following command to apply a specific stash entry, where `n` is the stash index `git stash apply n`.

```bash
git stash apply stash@{0}     # git stash apply stash@{n}
git stash apply 1             # for simpliticity
```

- Apply a stash and delete that stash. You can use the following command to pop a specific stash entry, where `n` is the stash index `git stash pop n`.

```bash
git stash pop
git stash pop 2
```

- Remove the latest stash entry from the stash list

```bash
git stash drop
git stash drop n
```

- Clear all stashes

```bash
git stash clear -
```

- Whenever we work on a new feature, but after coding for a while, you realize that you're in the main branch - not the branch you want to work on, but you're half code and you can't switch to other branches without commit. Git stash can come in handy. Just `git stash` the main branch, switch to that feature branch, then `git stash apply` or `git stash pop`.

```bash
git stash -m 'Your comment'         # when we're on main branch
git checkout feature/login
git stash pop 0
git add .
git commit -m 'Add login feature'
```

## See commits and history

```bash
git log
git log --stat      # show us the files that were changed within the commit
git log --oneline
git log --graph --oneline --decorate
```

- After `git log --oneline`, we can see the id for each commit. In order to comeback to these commits, use 3 commands below

```bash
git checkout af6b48c        # safe
git revert af6b48c          # sort of safe
git reset af6b48c           # unsafe. It can destroy the contents of a repository.
git reset af6b48c --hard    # go back to the commit with id af6b48c, take away commit history after it.
```

## Alias

```bash
alias graph= 'git log --all --decorate --oneline --graph'
```

## Squashing: combining multiple commits into one, for a cleaner git history

- How To Squash Your Git History Like A Pro
  https://www.youtube.com/watch?v=RwvTrSm7zEY

- With rebase workflow, we have more control.
  pick, reword, edit, squash, drop. Watch the video for better understanding.
  `pick` and `squash` are frequently used.

- With merge workflow, we only have a choice to squash all commits into one.

- Example: in `feature/login` branch, we could have 5 commits with some made up hash (auto-generated by git).

```bash
  f7f6f7d add login feature         # lastest commit in feature/login branch
  22tt66s add responsive login form
  a5f483d fix css bug
  310154h add css
  ddb214v add html login form (the oldest commit)
```

- When we want to merge feature/login into main branch. First, we need to be in main branch.
  It automatically adds changed files to staging area.

```bash
git switch main                   # or git checkout main
git pull origin main
git merge --squash feature/login
git commit -m 'your comment'
```

## Rebase

When HEAD pointer is on feature/...branches, feature/login or feature/cart for example, run

```bash
git rebase main
```
