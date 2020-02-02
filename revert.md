## Revert git add command with git reset to unstage or unindex files and folders

Assuming that you've staged/indexed some files and folders with git add and want to revert it without loosing your work. Let's revert it with git reset command. For more information, click git add and git reset links.

```sh
## Check the current status

inanzzz@inanzzz:~/project$ git status
On branch develop
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
 
	deleted:    src/AppBundle/AppBundle.php
 
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
 
	modified:   app/config/routing.yml
 
Untracked files:
  (use "git add <file>..." to include in what will be committed)
 
	src/Sport/

Stage/index files and folder by accident

inanzzz@inanzzz:~/project$ git add --all
inanzzz@inanzzz:~/project$ git status
On branch develop
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
 
	modified:   app/config/routing.yml
	deleted:    src/AppBundle/AppBundle.php
	new file:   DefaultController.php
```
## Unstage/Unindex files and folders

 Command below git reset applies to all files and folders but if you want to cover only one file then use git reset name-of-the-file command instead.

```sh
inanzzz@inanzzz:~/project$ git reset
Unstaged changes after reset:
M	app/config/routing.yml
D	src/AppBundle/AppBundle.php
D	src/AppBundle/Controller/DefaultController.php
inanzzz@inanzzz:~/project$ git status
On branch develop
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
 
	modified:   app/config/routing.yml
	deleted:    src/AppBundle/AppBundle.php
	deleted:    src/AppBundle/Controller/DefaultController.php
 
Untracked files:
  (use "git add <file>..." to include in what will be committed)
 
	src/Sport/
 
no changes added to commit (use "git add" and/or "git commit -a")

```