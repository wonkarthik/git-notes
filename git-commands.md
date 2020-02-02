
# Commands below are the most commonly used in daily working life. If you want to learn the best practises of branching model, make sure you read, understand and use git-flow cheatsheet and A successful [Git branching model](https://nvie.com/posts/a-successful-git-branching-model/).

```sh

git add file_name

Stages only given file. git add


git add --all

Stages all tracked and untracked files. git add


git add .

Stages all tracked and untracked files but ignores deleted files. git add


git add -u

Stages all tracked files but ignores untracked files. git add


git commit -m 'commit_message'

Commits all staged files. git commit


git merge branch_name

Merges given branch into current branch. git merge


git stash

Stashes all staged, tracked and untracked work in current branch. git stash


git stash apply

Brings back stashed work in current branch. git stash


git stash save

Copies all indexed files in a branch and pastes into another branch with git stash apply. git stash


git cherry-pick commit_id

Fetches changes of given commit into current branch. git cherry-pick


git branch -m current_branch_name new_branch_name

Renames branch. git branch


git checkout .

Undos changes and brings back deleted files in unstaged area. Files are removed from the working tree. Does not do anything to staged and untracked files. git checkout


git checkout -- .

Undos changes and brings back deleted files in unstaged area. Files are removed from the working tree. Does not do anything to staged and untracked files. git checkout


git checkout -- file_name

Undos changes to given file. File is removed from the working tree. Does not apply to untracked files. git checkout


git update-index --assume-unchanged file_name

Keeps the changes to given file and removes it from working tree. Does not apply to staged and untracked files. git update-index


git update-index --no-assume-unchanged file_name

Reverts what --assume-unchanged does. Does not apply to staged and untracked files. git update-index


git checkout branch_name file_name

Copies given file from given branch into the current branch. git checkout


git push origin --delete branch_name

Deletes given branch from remote repository. git push


git clean -f

Removes untracked files from working tree and the file system. Does not apply to staged and tracked files. git clean


git clean -fd

Removes untracked files and folders from working tree and the file system. Does not apply to staged and tracked files. git clean


git rm --cached file_name

Moves given file to untracked area by keeping the changes. File remains in file system. Flag -f is needed to move 'new files'. Does not apply to untracked files. git rm


git rm --force file_name

Removes given file from the file system and shows it in working tree. Does not apply to untracked files. git rm


git reset

Removes staged files and puts them back where they were before. Updates to files remain intact. git reset


git reset HEAD file_name

Removes given staged file and puts it back where it was before. Updates to file remain intact. git reset


git reset --soft HEAD~n or git reset --soft commit_id

Goes "n" (1,2,3...) times back in commit history and puts all the files back in staged area. Updates to files remain intact including in next commits. e.g. If gone back to commit 1 from last commit which is 3 and recommit all again, git history will not show commit 2 and 3 because they are now in commit 1. git reset


git reset --hard

Discards everything done in current branch. There is no going back to recover the loss. git reset


git reset --hard HEAD~n or git reset --hard commit_id

Goes "n" (1,2,3...) times back in commit history and discards everything done in given "n" branch (1,2,3). There is no going back to recover the loss. e.g. If gone back to commit 1 from last commit which is 3 there won't be anything in current working tree because everything has been discarded and git history will not show commit 2 and 3. git reset


git checkout -b branch_name commit_id

Creates a new branch based on a given commit. The hash-id above can be found with git reflog command. git checkout


git branch branch_name commit_id

Creates a new branch based on a given commit. The hash-id above can be found with git reflog command. git branch


git ls-remote git@github.com:Inanzzz/test.git master

Returns the latest commit id/hash of "master" branch. git-ls-remote


git show commit_id

Shows what a commit did. Outputs all changes line by line. git-show


git show commit_id --stat

Lists which files have been modified in a given commit. git-show


git log --follow -p file_name

Show all changes to a file in all commits. The most recent is on top. git-log


git push origin :name_of_the_remote_branch

Deletes given branch from remote repository. git-push


git remote add origin git@github.com:Your/remote-project.git

If you accidentally delete local copy of remote git information with rm -rf .git or an any another way, you'll get "fatal: 'origin' does not appear to be a git repository" and "fatal: Could not read from remote repository" error when trying to push local changes to remote repository. This command solves that issue. git-remote


git log --pretty=oneline

Unlike git log, this shows only commit IDs and the messages. git-log


git log --graph

Prints git commit history as in graphical presentation.

```