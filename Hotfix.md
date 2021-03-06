Hotfix branches are created to fix specific bugs in production environment which were introduced after deploying previous release branches. The main difference between hotfix and release branch is, hotfix branch branches off from master branch so it ignores everything (new features, code modifications, fixes, new files etc.) in develop branch. After finishing hotfix branches, they get merged back into develop and master branches so as a result both of these branches will have the fix immediately. We will see that below.


May branch off from master.

Must merge back into develop and master.

Branch naming convention is hotfix/x-x-x. The x[major release]-x[release]-x[hot-fix] signs represent the hotfix tag. e.g. If the current tag in your repository is "0.1.4" then your next tag will be "0.1.5" for hotfix branch. The one at the end gets bumped up by "1" so our new hotfix branch name should be hotfix/0.1.5. Next one will be hotfix/0.1.6.

When working with hotfix branches, you should open up a "pull request" in GitHub so that your team members can see what you're preparing to fix. This is considered as the best practise!

```
** Scenario

A few days after releasing release tag 0.1.0, I introduced some new files and features to develop branch. This is all normal for now. I suddenly realised that the message in 'one.txt' is wrong so I urgently need to change it.

```
Preparation

These steps are compulsory before start working on a new hotfix branch because our local branch might be behind remote copy.


Step 1

Make sure we're on develop branch.

```sh
$ git branch
* develop
  master

Step 2

Fetch all remote updates.


$ git remote update
Fetching origin
remote: Counting objects: 1, done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From github.com:inanzzz/manual
   7d173b0..53353d6  develop    -> origin/develop

Step 3

Update local develop branch so it is up-to-date with remote copy.


$ git pull origin develop
From github.com:inanzzz/manual
 * branch            develop    -> FETCH_HEAD
Updating 7d173b0..53353d6
Fast-forward
 one.txt | 2 ++
 two.txt | 1 +
 2 files changed, 3 insertions(+)
 create mode 100644 two.txt

Step 4

Checkout to master branch.


$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

Step 5

Update local master branch so it is up-to-date with remote copy.


$ git pull origin master
From github.com:inanzzz/manual
 * branch            master     -> FETCH_HEAD
Already up-to-date.

Create hotfix branch

Step 1

Check the current git status. As you can see below, master branch is behind develop branch at the moment.


$ git branch -avv
  develop                            53353d6 [origin/develop] Merge pull request #3 from inanzzz/feature/hello-mars
* master                             7d173b0 [origin/master] Merge pull request #1 from inanzzz/feature/hello-world
  remotes/origin/develop             53353d6 Merge pull request #3 from inanzzz/feature/hello-mars
  remotes/origin/feature/hello-mars  46fbd1b New feature updates
  remotes/origin/feature/hello-world 6a26393 Feature hello-world commit
  remotes/origin/master              7d173b0 Merge pull request #1 from inanzzz/feature/hello-world



As you can see above, right after release tag 0.1.0*, there has been some development took place and it was merged back into develop branch which is fine because hotfix is not interested in what we have in develop branch.


Step 2

Create a hotfix branch that branches off of local master branch and tracks origin/master.


$ git checkout -b hotfix/0.1.1 origin/master
Branch hotfix/0.1.1 set up to track remote branch master from origin.
Switched to a new branch 'hotfix/0.1.1'

$ git branch
  develop
* hotfix/0.1.1
  master

Step 3

Fix the bug and commit to it.


$ cat one.txt 
feature/hello-world

$ echo 'feature/hello-inanzzz' > one.txt
$ git add --all
$ git commit -m 'I just fixed a bug'
[hotfix/0.1.1 8ed4ad7] I just fixed a bug
 1 file changed, 1 insertion(+), 1 deletion(-)

$ cat one.txt 
feature/hello-inanzzz

Step 4

Push hotfix branch to remote repository.


$ git push origin hotfix/0.1.1
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 312 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:inanzzz/manual.git
   7d173b0..8ed4ad7  hotfix/0.1.1 -> hotfix/0.1.1

Step 5

If you go to GitHub, there will be a notification bar that will ask you to open a new "pull request" for the hotfix branch you've just pushed. Open it by comparing it to master branch, writing a subject and a description for it.



Step 6

At this point "peer review" takes place against the "pull request" in GitHub. If everyone in your team is happy with the work you've done in hotfix branch, there is nothing to worry about otherwise you keep working to make everyone happy. This process just shows everyone what will be fixed. Do not use "Merge pull request" button.


Step 7

Checkout into master branch.


$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

$ git branch
  develop
* master
  hotfix/0.1.1

Step 8

Merge hotfix branch into master branch. Do not use --no-ff flag otherwise merge will use "recursive" strategy instead of "fast-forward" and this will lead GitHub to create a "pull request" notification after pushing master branch to remote which is an unwanted behavior.


$ git merge hotfix/0.1.1
Updating 7d173b0..8ed4ad7
Fast-forward
 one.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

Step 9

Tag the hotfix point by creating a new tag.


$ git tag -a 0.1.1 -m 'Create hotfix tag 0.1.1'

Step 10

Verify that the tag has been created.


$ git tag
0.1.0
0.1.1



Step 11

Push master branch to remote repository. In GitHub, this will also merge and close the "pull request" of remote hotfix branch into master branch however it won't delete it. You'll see that in GitHub. Also, you will be notified to create a "pull request" for master branch but ignore it for now. It will disappear after pushing develop branch to remote repository later on.


$ git push origin master
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:inanzzz/manual.git
   7d173b0..8ed4ad7  master -> master

Step 12

Push the tags to remote repository. If you go to GitHub, you'll see the tag under "Release" tab.


$ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 180 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:inanzzz/manual.git
 * [new tag]         0.1.1 -> 0.1.1



Step 13

Checkout into develop branch.


$ git checkout develop
Switched to branch 'develop'
Your branch is up-to-date with 'origin/develop'.

$ git branch
* develop
  master
  hotfix/0.1.1

Step 14

Merge hotfix branch into develop branch. We did some work on file called 'one.txt' in develop branch after creating a release branch while ago so 'one.txt' in develop branch is more up-to-date than the one in master branch. We need to resolve conflicts manually and commit to it.


$ git merge hotfix/0.1.1
Auto-merging one.txt
CONFLICT (content): Merge conflict in one.txt
Automatic merge failed; fix conflicts and then commit the result.

# Conflict
$ cat one.txt 
feature/hello-inanzzz

# Resolved
$ cat one.txt 
feature/hello-inanzzz
feature/hello-mars
feature/hello-jupiter

Step 15

Push develop branch to remote repository.


$ git push origin develop
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 389 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:inanzzz/manual.git
   53353d6..a2a8dba  develop -> develop

Step 16

Remove hotfix branch from the local repository.


$ git branch -D hotfix/0.1.1
Deleted branch hotfix/0.1.1 (was 8ed4ad7).

$ git branch
* develop
  master

Step 17

Remove hotfix branch from the remote repository.


$ git push origin :hotfix/0.1.1
To git@github.com:inanzzz/manual.git
 - [deleted]         hotfix/0.1.1

Check the current git status. As you can see below, master branch and develop branch are not even.


$ git branch -avv
* develop                            a2a8dba [origin/develop] Resolved conflicts
  master                             8ed4ad7 [origin/master] I just fixed a bug
  remotes/origin/develop             a2a8dba Resolved conflicts
  remotes/origin/feature/hello-mars  46fbd1b New feature updates
  remotes/origin/feature/hello-world 6a26393 Feature hello-world commit
  remotes/origin/master              8ed4ad7 I just fixed a bug



Step 18

If you go to GitHub, you'll should see cases below happened.


The master and develop branches are not even.

The hotfix tag "0.1.1" is there.

The hotfix branch itself is deleted.

The hotfix "pull request" that we've opened is deleted.

Deployment

In the case deployment, you should checkout into tag number and deploy it.


$ git remote update
$ git checkout 0.1.1
$ git pull origin 0.1.1
$ cap production deploy

```
```sh
## Overview 

# 1. Checked out into develop branch
git checkout develop
 
# 2. Fetched all remote updates
git remote update
 
# 3. Update local develop branch with remote copy
git pull origin develop
 
# 4. Checked out into master branch
git checkout master
 
# 5. Update local master branch with remote copy
git pull origin master
 
# 6. Created a hotfix branch that tracks origin/master
git checkout -b hotfix/0.1.1 origin/master
 
# 7. Did some fixes and committed to it
 
# 8. Pushed hotfix branch to remote repository
git push origin hotfix/0.1.1
 
# 9. Opened a "pull request" in GitHub for team to verify the hotfix
 
# 10. Checkout into master branch
git checkout master
 
# 11. Merged hotfix branch into master branch
git merge hotfix/0.1.1
 
# 12. Tagged the hotfix point by creating a new tag
git tag -a 0.1.1 -m 'Create hotfix tag 0.1.1'
 
# 13. Pushed master branch to remote repository
git push origin master
 
# 14. Pushed the tags to remote repository
git push origin --tags
 
# 15. Checkout into develop branch
git checkout develop
 
# 16. Merged hotfix branch into develop branch
git merge hotfix/0.1.1
 
# 17. Pushed develop branch to remote repository
git push origin develop
 
# 18. Removed hotfix branch from the local repository
git branch -D hotfix/0.1.1
 
# 19. Removed hotfix branch from the remote repository
git push origin :hotfix/0.1.1

```