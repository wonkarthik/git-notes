## Setting up a new git project from scratch

In this example, we're going to set up a new git project repository and make it ready for development in our local environment.

```sh
GitHub setup

I assume that you already have set up SSH connection between GithHub account and your local environment. Create an empty repository called "manual" in GitHub account.


Clone repository

$ git clone git@github.com:inanzzz/manual.git
Cloning into 'manual'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
 
$ cd manual/

Create master branch

Our aim here is to create a local master branch first and push it to remote repository so it exists in GitHub. At the end, it will track origin/master.


Step 1

Create a README.md file and commit to it. This will automatically create master branch in your local repository.


$ echo "# manual" > README.md
$ git add --all
$ git commit -m 'Very first commit'
[master (root-commit) 43686f8] Very first commit
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
 
$ git branch
* master

Step 2

Push it to remote repository. You must use -u flag at the first time that you push that branch so that it tracks origin/master.


$ git push -u origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 234 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:inanzzz/manual.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.

Step 3

Run command below to see if everything is set up perfectly. Also, if you go to GitHub account, you'll see that the master branch has been created.


$ git branch -avv
* master                0d0cca9 [origin/master] Very first commit
  remotes/origin/master 0d0cca9 Very first commit
```


## Create develop branch

Our aim here is to create a local develop branch first and push it to remote repository so it exists in GitHub. At the end, it will track origin/develop.

```sh
Step 1

Create local develop branch.


$ git checkout -b develop
Switched to a new branch 'develop'
 
$ git branch
* develop
  master

Step 2

Push it to remote repository. You must use -u flag at the first time that you push that branch so that it tracks origin/develop.


$ git push -u origin develop
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:inanzzz/manual.git
 * [new branch]      develop -> develop
Branch develop set up to track remote branch develop from origin.

Step 3

Run command below to see if everything is set up perfectly. Also, if you go to GitHub account, you'll see that the develop branch has been created.


$ git branch -avv
* develop                0d0cca9 [origin/develop] Very first commit
  master                 0d0cca9 [origin/master] Very first commit
  remotes/origin/develop 0d0cca9 Very first commit
  remotes/origin/master  0d0cca9 Very first commit

```

Final
```sh
After completing steps above, you should set develop branch as "default" branch in GitHub so do the following in GitHub account.


Select "Settings" tab on top.

Select "Branches" menu option on the left.

Change master to develop in dropdown of "Default branch" section.

Hit "Update" button and accept the notification question.

The reason why we should do this is because, project development is always based on develop branch. This is the best practise!

```

## Overview

In short terms, this is what we did above.
```sh 

# 1. Manually created a remote repository in GitHub
 
# 2. Cloned remote repository to local environment
git clone git@github.com:inanzzz/manual.git
 
# 3. Created a local master branch by adding a README.md file
echo "# manual" > README.md
git add --all
git commit -m 'Very first commit'
 
# 4. Pushed master branch to remote repository
git push -u origin master
 
# 5. Created a local develop branch
git checkout -b develop
 
# 6. Pushed develop branch to remote repository
git push -u origin develop
 
# 7. Manually set develop branch as "default" branch in GitHub
GitHub > Settings > Branches > Develop > Update

```