## Squashing many commits into one commit with interactive git rebase

When you have many commit messages, it is sometimes hard to follow so you might want to reduce the amount by using interative rebasing which is what we're going to do here. Squashing Commits page.


The rule

Do not use rebase for "public" feature branches where more than one developer works on. It is used only for "private" feature branches where only one developer works on.


Note:

If you get rid of undone/unfinished rebase work, you can remove rebase history with rm -fr .git/rebase-merge command.

```sh
Current commit history

$ git log --pretty=oneline
2121c615f9e0b53abc6fc06e3bb65f7932660e82 Very last commit
d499651137df9fa2168a0816897024ce2e996c21 Update 5 commit message
747c32b71f8bafea691dd8e08626af00c2f33242 Update 4 commit message
33ca8ba79e591a83aca89e364d0c2fdc46828827 Update 3 commit message
5f9a532c8f09d58cb77495c5ab2493f25413cf3a Update 2 commit message
d78dc4d0f4a6d4c085106c66de211061796b6682 Update 1 commit message
3dcf60f4a39c10b5f61e4da58fc71efb785426a9 Very first commit

Dummy file

Commits above represent these changes in our dummy file so, we're expecting not to lose any of these updates after squashing process.


$ cat README.md
Very first commit
Update 1
Update 2
Update 3
Update 4
Update 5
Very last commit

Squash

Say you want to combine commits 2-3-4 into a single one. By counting from top to bottom, you should go one step earlier of your earliest commit selection so in this case it will be commit Update 5 which is on HEAD 6. If you don't go one step earlier, you'll get "Cannot 'squash' without a previous commit" error and lose your work after exiting from the editor. Update file below as shown.


$ git rebase -i HEAD~6
 
# Mark commits that you want to squash with "squash" key as shown below. Make sure the one on top remains intact otherwise you'll get error above. Selected commits will be squashed into the one on top which is "d78dc4d Update 1 commit message".
pick d78dc4d Update 1 commit message
squash 5f9a532 Update 2 commit message
squash 33ca8ba Update 3 commit message
squash 747c32b Update 4 commit message
pick d499651 Update 5 commit message
pick 2121c61 Very last commit
 
# Rebase 3dcf60f..2121c61 onto 3dcf60f
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out

After saving and exiting from editor above, it will open up an another editor that will present message below. No need to update this file.


# This is a combination of 4 commits.
# The first commit's message is:
Update 1 commit message
 
# This is the 2nd commit message:
 
Update 2 commit message
 
# This is the 3rd commit message:
 
Update 3 commit message
 
# This is the 4th commit message:
 
Update 4 commit message
 
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# rebase in progress; onto 3dcf60f
# You are currently editing a commit while rebasing branch 'master' on '3dcf60f'.
#
# Changes to be committed:
#       modified:   README.md
#

Save and exit from this editor as well. Result will be as follows.


[detached HEAD 9713b52] Update 1 commit message
 1 file changed, 5 insertions(+), 1 deletion(-)
Successfully rebased and updated refs/heads/master.

Result

As you can see, commits 2-3-4 have been squashed into Update 1 commit message. You might verify with git show 9713b526703ae596c083da7a6b1f957b6c72c210 command.


$ git log --pretty=oneline
66a80d94ed766507c7832aa96eff3d754e06d526 Very last commit
9422ed432b439b93b22dd470b2ab392286046fc6 Update 5 commit message
9713b526703ae596c083da7a6b1f957b6c72c210 Update 1 commit message
3dcf60f4a39c10b5f61e4da58fc71efb785426a9 Very first commit

Dummy file

We kept all the updates after squashing process.


$ cat README.md
Very first commit
Update 1
Update 2
Update 3
Update 4
Update 5
Very last commit
```