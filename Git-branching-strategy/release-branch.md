## Working with git release branches

Release branches contain production ready new features and bug fixes that come from stable develop branch. In most cases, master branch is always behind develop branch because development goes on develop branch. After finishing release branches, they get merged back into develop and master branches so as a result both of these branches will match each other eventually. We will see that below.


May branch off from develop.

Must merge back into develop and master.

Branch naming convention is release/x-x-x. The x[major release]-x[release]-x[hot-fix] signs represent the release tag. e.g. If the current tag in your repository is "0.1.4" then your next tag will be "0.2.0" for release branch. The one in the middle gets bumped up by "1" and the last one gets reset to "0" so our new release branch name should be release/0.2.0. Next one will be release/0.3.0.

When working with release branches, you should open up a "pull request" in GitHub so that your team members can see what you're preparing to release. This is considered as the best practise!


Preparation

These steps are compulsory before start working on a new release branch because our local branch might be behind remote copy.

```sh
Step 1

Make sure we're on develop branch.


$ git branch
* develop
  master

Step 2

Fetch all remote updates.


$ git remote update
Fetching origin

Step 3

Update local develop branch so it is up-to-date with remote copy.


$ git pull origin develop
From github.com:inanzzz/manual
 * branch            develop    -> FETCH_HEAD
Already up-to-date.
```
## Create release branch

```sh
Step 1

Check the current git status. As you can see below, master branch is behind develop branch at the moment.


$ git branch -avv
* develop                            d99ca8a [origin/develop] Merge pull request #1 from inanzzz/feature/hello-world
  master                             2f94f7d [origin/master] Very first commit
  remotes/origin/develop             d99ca8a Merge pull request #1 from inanzzz/feature/hello-world
  remotes/origin/feature/hello-world 5a93e5a Feature hello-world commit
  remotes/origin/master              2f94f7d Very first commit



Step 2

Create a release branch that branches off of local develop branch and tracks origin/develop.


$ git checkout -b release/0.1.0 origin/develop
Branch release/0.1.0 set up to track remote branch develop from origin.
Switched to a new branch 'release/0.1.0'

$ git branch
  develop
  master
* release/0.1.0

Step 3

Push release branch to remote repository.


$ git push origin release/0.1.0
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:inanzzz/manual.git
 * [new branch]      release/0.1.0 -> release/0.1.0

Step 4

If you go to GitHub, unlike feature branches, there won't be a notification bar waiting for you to open a new "pull request" for the release branch you've just pushed so you need to do it manually instead. To open a "pull request" for the release branch, hit "New pull request" button, compare master (base dropdown) branch to release/0.1.0 (compare dropdown) branch, write a subject and a description for it. This will open a "pull request" so that it can be reviewed by other team members. If what commits you're preparing to release are fine for the rest of the team members then there is nothing to worry about. This process just shows everyone what will be released. Do not use "Merge pull request" button.




Step 5

Checkout into master branch.


$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

$ git branch
  develop
* master
  release/0.1.0

Step 6

Update local master branch.


$ git pull origin master
From github.com:inanzzz/manual
 * branch            master     -> FETCH_HEAD
Already up-to-date.

Step 7

Merge release branch into master branch. Do not use --no-ff flag otherwise merge will use "recursive" strategy instead of "fast-forward" and this will lead GitHub to create a "pull request" notification after pushing master branch to remote which is an unwanted behavior.


$ git merge release/0.1.0
Updating 2f94f7d..d99ca8a
Fast-forward
 one.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 one.txt

Step 8

Tag the release point by creating a new tag.


$ git tag -a 0.1.0 -m 'Create release tag 0.1.0'

Step 9

Verify that the tag has been created.


$ git tag
0.1.0



Step 10

Push master branch to remote repository. In GitHub, this will also merge and close the "pull request" of remote release branch into master branch however it won't delete it. You'll see that in GitHub.


$ git push origin master
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:inanzzz/manual.git
   2f94f7d..d99ca8a  master -> master

Step 11

Push the tags to remote repository. If you go to GitHub, you'll see the tag under "Release" tab.


$ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 179 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:inanzzz/manual.git
 * [new tag]         0.1.0 -> 0.1.0



Step 12

Checkout into develop branch.


$ git checkout develop
Switched to branch 'develop'
Your branch is up-to-date with 'origin/develop'.

$ git branch
* develop
  master
  release/0.1.0

Step 13

Merge release branch into develop branch.


$ git merge release/0.1.0
Already up-to-date.

Step 14

Push develop branch to remote repository.


$ git push origin develop
Everything up-to-date

Step 15

Remove release branch from the local repository.


$ git branch -D release/0.1.0
Deleted branch release/0.1.0 (was d99ca8a).

$ git branch
* develop
  master

Step 16

Remove release branch from the remote repository.


$ git push origin :release/0.1.0
To git@github.com:inanzzz/manual.git
 - [deleted]         release/0.1.0

Check the current git status. As you can see below, master branch and develop branch are even now.


$ git branch -avv
* develop                            d99ca8a [origin/develop] Merge pull request #1 from inanzzz/feature/hello-world
  master                             d99ca8a [origin/master] Merge pull request #1 from inanzzz/feature/hello-world
  remotes/origin/develop             d99ca8a Merge pull request #1 from inanzzz/feature/hello-world
  remotes/origin/feature/hello-world 5a93e5a Feature hello-world commit
  remotes/origin/master              d99ca8a Merge pull request #1 from inanzzz/feature/hello-world



Step 17

If you go to GitHub, you'll should see cases below happened.


The master and develop branches are even.

The release tag "0.1.0" is there.

The release branch itself is deleted.

The release "pull request" that we've opened is deleted.
```
## Deployment
```sh
In the case deployment, you should checkout into tag number and deploy it.


$ git remote update
$ git checkout 0.1.0
$ git pull origin 0.1.0
$ cap production deploy
```

```sh
Overview

In short terms, this is what we did above.


# 1. Checked out into develop branch
git checkout develop
 
# 2. Fetched all remote updates
git remote update
 
# 3. Update local develop branch with remote copy
git pull origin develop
 
# 4. Created a release branch that tracks origin/develop
git checkout -b release/0.1.0 origin/develop
 
# 5. Pushed release branch to remote repository
git push origin release/0.1.0
 
# 6. Opened a "pull request" in GitHub for team to verify the release
 
# 7. Checkout into master branch
git checkout master
 
# 8. Updated local master branch with remote copy
git pull origin master
 
# 9. Merged release branch into master branch
git merge release/0.1.0
 
# 10. Tagged the release point by creating a new tag
git tag -a 0.1.0 -m 'Create release tag 0.1.0'
 
# 11. Pushed master branch to remote repository
git push origin master
 
# 12. Pushed the tags to remote repository
git push origin --tags
 
# 13. Checkout into develop branch
git checkout develop
 
# 14. Merged release branch into develop branch
git merge release/0.1.0
 
# 15. Pushed develop branch to remote repository
git push origin develop
 
# 16. Removed release branch from the local repository
git branch -D release/0.1.0
 
# 17. Removed release branch from the remote repository
git push origin :release/0.1.0

```