## Some useful git branching notes

### These are some notes related to git branches.


* If you're planning to use gitflow, make sure to use gitflow-avh version because the original one is buggy and not maintained anymore. Mac OS users; install it with brew install git-flow-avh.

* The origin/master is considered to be the main branch and its source code is always in a production-ready state.

* The origin/`develop` is considered to be the `develop`ment branch and its source code is always in "work in progress" state for the next release.

* When the source code in the `develop` branch is stable and ready to be released, it should be merged into master branch and be tagged with a release number.

* When merging release and hotfix into master branch, tagging takes place in master branch not in `develop`. Tags represents project's current state so they are version numbers. There is no tagging involved in feature branches.

* The command git pull would work only if the branch you have checked out is tracking an remote branch. For example; if the branch you have checked out tracks origin/`develop`, git pull is equivalent to git pull origin `develop`.

* Feature branches branch off from/track `develop` and merged back into `develop` branch.

* Release branches branch off from/track `develop` and merged back into `develop` as well as master branch.

* Hotfix branches branch off from/track master and merged back into `develop` as well as master branch.