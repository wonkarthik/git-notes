## Reset all changes to previous commit with git reset --hard

You have done some updates to files, created or deleted files/folders so on. but want to get rid of all of it for some reason and go back to previous commit with git reset --hard command. 


## List your previous commits
```sh
The one on top is always the most recent commit head. For more information.


inanzzz@inanzzz:~/project$ git log
commit 63de9265c4a3140ce1bbc6c271e1ee27cee487a5
Author: inanzzz my@email.com
Date:   Sat Mar 7 18:46:19 2015 +0000
 
    Just committed
 
commit 3ee42f91dbf877d9b3c048aef3d378c403650217
Author: inanzzz my@email.com
Date:   Fri Mar 6 22:33:19 2015 +0000
 
    First commit

Check the current status

inanzzz@inanzzz:~/project$ git status
On branch develop
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
 
	deleted:    SportFootballBundle.php
 
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
 
	modified:   app/AppKernel.php
 
Untracked files:
  (use "git add <file>..." to include in what will be committed)
 
	AnotherController.php

Stage/index your files

inanzzz@inanzzz:~/project$ git add --all
inanzzz@inanzzz:~/project$ git status
On branch develop
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
 
	modified:   app/AppKernel.php
	new file:   AnotherController.php
	deleted:    SportFootballBundle.php

Revert all changes

inanzzz@inanzzz:~/project$ git reset --hard
HEAD is now at 63de926 Just committed
inanzzz@inanzzz:~/project$ git status
On branch develop
nothing to commit, working directory clean
```