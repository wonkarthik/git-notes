This is post shows just the common or plain practice of pushing our local work to remote repository. There should always be a "master" and "develop" branch in your project. Any work you do comes out of "develop" branch. Depending on the way your team works, you would often have two options. One: your "feature" branch gets merged into "develop" in your local PC and "develop" gets pushed to remote. Two: your "feature" branch gets pushed to remote and then gets merged to "develop" after your team members' reviews. I used both versions but prefer the second option because before merging your work to develop, your team agrees on your code, or may be not! Then you either merge it or re-factor it which is a "good practice".


## Full example for option two

```sh
inanzzz@inanzzz:~/project$ git branch
master
* develop
inanzzz@inanzzz:~/project$ git status
# if there is something then commit
inanzzz@inanzzz:~/project$ git remote update
inanzzz@inanzzz:~/project$ git pull origin develop
# if there is conflicts then resolve
inanzzz@inanzzz:~/project$ git checkout -b my-feature-branch develop
inanzzz@inanzzz:~/project$ git branch
master
develop
* my-feature-branch
# do what you do and commit
inanzzz@inanzzz:~/project$ git checkout develop
inanzzz@inanzzz:~/project$ git merge my-feature-branch
inanzzz@inanzzz:~/project$ git pull origin develop
# if there is conflicts then resolve
inanzzz@inanzzz:~/project$ git push origin develop
```
## Full example for option one

```sh
inanzzz@inanzzz:~/project$ git branch
master
* develop
inanzzz@inanzzz:~/project$ git status
# if there is something then commit
inanzzz@inanzzz:~/project$ git remote update
inanzzz@inanzzz:~/project$ git pull origin develop
# if there is conflicts then resolve
inanzzz@inanzzz:~/project$ git checkout -b my-feature-branch develop
inanzzz@inanzzz:~/project$ git branch
master
develop
* my-feature-branch
# do what you do and commit
inanzzz@inanzzz:~/project$ git push origin my-feature-branch
# create your pull request and let people review it.
# if they like it then merge it, if not then re-factor it

```