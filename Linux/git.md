# Git

## installing git:

```
sudo pacman -S git
```


## configurations:

```
# set the default user naem ...
git config --global user.name "<user-name-here>"
# set the default email ...
git config --global user.email "<user-email-here>"
# set the default editor for long commit messages...
git config --global core.editor "<editor-of-choice-here>"
# setting up difference checking tool
git config --global diff.tool <tool-here>
# set and unset the cache to save your access token instead of memorising it...
git config --global credential.helper cache
# unsetting the saved cache ...
git config --global --unset credential.helper

```

## git manipulating git locally:

```
# initilizing a git repository...
git init
# checking the past commits
git log
#log with a graph... (of two branches)
git log --graph --oneline <branch> <branch>
# checking out a different commit
git checkout <commit-id>
# check status of the current repository...
git status
# adding files to the up coming commit... dot to include everything
git add <file-or-folder>
# removing files from the upcoming commit... dot to include everything
git revert <file-or-folder>



```
### branch manipulations:

```

#creating a new branch...
git branch <branch-name-here>
#checking out a different branch..
git checkout <branch-name>
#  after checking out a branch you can merge into it using...
git merge <second-branch-name>
# you can also merge two branches like this ...(first one is the destination)
git merge <first-branch-name> <second-branch-name>
# get the commits that are causing a conflict...
git log --merge
# helps to identify the differences between the states repositories or files.
git diff
# git chekcout command is used to undo the changes made to the file, or for changing branches.
git checkout
# git mixed it used to undo changes to the working directory and staging area.
git reset --mixed
# git merge abort helps in exiting the merge process and returning back to the state before the merging began.
git merge --abort
# the reset command is used at the time of merge conflict to reset the conflicted files to their original state.
git reset || git reset --hard origin/branch
# showing the changes in each commit in one branch
git show <branch-name>
# to delete a branch use
git branch -d <branch-name>
```
### git remote manipulations:

```
# add a remote to the repository...
git remote add <remote-name> <url>
# remove a remote...
git remote rm <remote-name>
# display all remotes...(with their urls)
git remote -v
#push all new local commits to the cloud...
git push -u <remote-name> <branch-name>
# pull all changes from the cloud...
git pull



```
