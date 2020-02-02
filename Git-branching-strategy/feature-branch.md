## Working with git feature branches

Feature branches are used to introduce new features, remove existing features and fixing bugs for next release. Since they get merged back into develop branch, master branch will always remain behind develop branch in both local and remote repositories.


* May branch off from develop.

* Must merge back into develop.

* Branch naming convention is feature/xxx-xxx-xxx. e.g. feature/hello-world

When working with feature branches, you should open up a "pull request" in GitHub so that your team members can "peer review" your work. This is considered as the best practise!


### Preparation

These steps are compulsory before start working on a new feature branch because our local branch might be behind remote copy.

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

Create feature branch

Step 1

Create it so that it tracks origin/develop.


$ git checkout -b feature/hello-world origin/develop
Branch feature/hello-world set up to track remote branch develop from origin.
Switched to a new branch 'feature/hello-world'

$ git branch
  develop
* feature/hello-world
  master

Step 2

Assume that you did some work in your project so now commit what you've done.


$ echo 'feature/hello-world' > one.txt
$ git add --all
$ git commit -m 'Feature hello-world commit'
[feature/hello-world 47645b3] Feature hello-world commit
 1 file changed, 1 insertion(+)
 create mode 100644 one.txt



Step 3

Push it to remote repository to open a "pull request".


$ git push origin feature/hello-world
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 313 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:inanzzz/manual.git
 * [new branch]      feature/hello-world -> feature/hello-world

Step 4

If you go to GitHub, there will be a notification bar that will ask you to open a new "pull request" for the feature branch you've just pushed. Open it by comparing it to develop branch, writing a subject and a description for it.






Step 5

At this point "peer review" takes place against the "pull request" in GitHub. If everyone in your team is happy with the work you've done in feature branch, you can merge it to develop branch in GitHub and delete it unless you need to do some kind of modifications to make everyone happy first. If all go well, then you can merge it manually by hitting "Merge pull request" button and and then hit "Delete pull request" button to finish off your work. Let's say you merged and deleted it in GitHub however, it only applies to remote repository. You must now reflect what you've done in GitHub to your local develop branch because it is behind remote develop branch.


Step 6

Checkout into develop branch.


$ git checkout develop
Switched to branch 'develop'
Your branch is up-to-date with 'origin/develop'.

$ git branch
* develop
  feature/hello-world
  master

Step 7

Delete local feature branch like you did in GitHub before.


$ git branch -D feature/hello-world
Deleted branch feature/hello-world (was 47645b3).

$ git branch
* develop
  master

Step 8

Just to confirm that your local develop still doesn't have the merged changes yet. As we said above, all you have done was in GitHub, not in in your local repository. This confirms it!


$ git branch -avv
* develop                            e0d2b2e [origin/develop] Very first commit
  master                             e0d2b2e [origin/master] Very first commit
  remotes/origin/develop             e0d2b2e Very first commit
  remotes/origin/feature/hello-world 0dacd74 Feature hello-world commit
  remotes/origin/master              e0d2b2e Very first commit



Step 9

Fetch all remote updates.


$ git remote update
Fetching origin
remote: Counting objects: 1, done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From github.com:inanzzz/manual
   e0d2b2e..b326329  develop    -> origin/develop

Step 10

Update your local develop so it is up-to-date with remote copy.


$ git pull origin develop
From github.com:inanzzz/manual
 * branch            develop    -> FETCH_HEAD
Updating e0d2b2e..b326329
Fast-forward
 one.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 one.txt

Just to confirm that your local develop branch is now up-to-date with the remote develop branch. This confirms it!


$ git branch -avv
* develop                            b326329 [origin/develop] Merge pull request #1 from inanzzz/feature/hello-world
  master                             e0d2b2e [origin/master] Very first commit
  remotes/origin/develop             b326329 Merge pull request #1 from inanzzz/feature/hello-world
  remotes/origin/feature/hello-world 0dacd74 Feature hello-world commit
  remotes/origin/master              e0d2b2e Very first commit

```

### Overview

In short terms, this is what we did above.

```sh

# 1. Checked out into develop branch
git checkout develop
 
# 2. Fetched all remote updates
git remote update
 
# 3. Update local develop branch with remote copy
git pull origin develop
 
# 4. Created a feature branch that tracks origin/develop
git checkout -b feature/hello-world origin/develop
 
# 5. Did some dummy work
echo 'feature/hello-world' > one.txt
git add --all
git commit -m 'Feature hello-world commit'
 
# 6. Pushed feature branch to remote repository
git push origin feature/hello-world
 
# 7. Opened a "pull request" in GitHub for "peer review"
 
# 8. Merged and deleted feature branch in GitHub
 
# 9. Checked out into develop branch
git checkout develop
 
# 10. Delete local feature branch
git branch -D feature/hello-world
 
# 11. Fetched all remote updates
git remote update
 
# 12. Update local develop branch wit remote copy
git pull origin develop

```