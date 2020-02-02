## Keeping the work with git stash without committing and go to work in different branch for urgent request

There is an urgent request comes in like bug fix and you have to switch to it but don't want to commit or lose your work in your current working branch. This is where git stash comes in handy. 

## Git stash

```sh
inanzzz@inanzzz:~/project$ git branch
  develop
* my-feature-branch
inanzzz@inanzzz:~/project$ git status
On branch my-feature-branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
 
	modified:   file_one.txt
	modified:   file_two.txt
 
no changes added to commit (use "git add" and/or "git commit -a")
inanzzz@inanzzz:~/project$ git stash
Saved working directory and index state WIP on my-feature-branch: 860fcb2 Commit
HEAD is now at 860fcb2 Commit
inanzzz@inanzzz:~/project$ git status
On branch my-feature-branch
nothing to commit, working directory clean

Do other urgent work

Checkout to "develop" and do what ever you have to do. You may create a branch to work etc. and push it.


inanzzz@inanzzz:~/project$ git checkout develop
Switched to branch 'develop'
inanzzz@inanzzz:~/project$ git branch
* develop
  my-feature-branch

Go back to original branch

We're back where we were and recover from git stash with git stash apply.


inanzzz@inanzzz:~/project$ git checkout my-feature-branch 
Switched to branch 'my-feature-branch'
inanzzz@inanzzz:~/project$ git status
On branch my-feature-branch
nothing to commit, working directory clean
inanzzz@inanzzz:~/project$ git stash apply
On branch my-feature-branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
 
	modified:   file_one.txt
	modified:   file_two.txt
 
no changes added to commit (use "git add" and/or "git commit -a")

```

## Transferring all indexed files and folders from one branch to another with git stash

You know that some indexed files and folder structure is old in a branch so you want to get the new versions from another. For that, we use git stash command

```sh
## Check current status

inanzzz@inanzzz:~/project$ git branch
  branch-one
* branch-two
  develop
inanzzz@inanzzz:~/project$ git status
On branch branch-two
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
 
	new file:   dir-one/hello_one.txt
	modified:   file_one.txt
	deleted:    file_seven.txt
	modified:   file_two.txt

Save the changes

Saving the state of all the changes so we don't lose anything.


inanzzz@inanzzz:~/project$ git stash save
Saved working directory and index state WIP on branch-two: a08b95e First commit in branch-two branch
HEAD is now at a08b95e First commit in branch-two branch
inanzzz@inanzzz:~/project$ git status
On branch branch-two
nothing to commit, working directory clean

Switch branch

Switch to where we want to transfer our saved state.


inanzzz@inanzzz:~/project$ git checkout branch-one 
Switched to branch 'branch-one'
inanzzz@inanzzz:~/project$ git status
On branch branch-one
nothing to commit, working directory clean

Transfer the changes

Once all the conflicts resolved, job is done.


inanzzz@inanzzz:~/project$ git stash apply
Auto-merging file_two.txt
CONFLICT (content): Merge conflict in file_two.txt
Removing file_seven.txt
Auto-merging file_one.txt
CONFLICT (content): Merge conflict in file_one.txt

Check current status

inanzzz@inanzzz:~/project$ git status
On branch branch-one
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
 
	new file:   dir-one/hello_one.txt
	deleted:    file_seven.txt
 
Unmerged paths:
  (use "git reset HEAD <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
 
	both modified:      file_one.txt
	both modified:      file_two.txt
 ```   