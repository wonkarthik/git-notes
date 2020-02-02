How to recover deleted git branch

If you want to recover a deleted branch then follow the steps below.

## Current status
```sh
inanzzz-MBP:sport inanzzz$ git branch
  develop
  entities
  fixtures
  master
* relationships
```
## Delete branch
```sh
inanzzz-MBP:sport inanzzz$ git checkout develop
Switched to branch 'develop'
inanzzz-MBP:sport inanzzz$ git branch -D relationships
Deleted branch relationships (was 6d7ad85).
inanzzz-MBP:sport inanzzz$ git branch
* develop
  entities
  fixtures
  master
```
## List reference logs
```sh
inanzzz-MBP:sport inanzzz$ git reflog
7d5715c HEAD@{0}: checkout: moving from develop to crud
7d5715c HEAD@{1}: checkout: moving from relationships to develop
6d7ad85 HEAD@{2}: commit: Lazy load finished
7d5715c HEAD@{3}: checkout: moving from develop to relationships
7d5715c HEAD@{4}: merge entities-fixtures: Fast-forward
c974044 HEAD@{5}: checkout: moving from entities-fixtures to develop
7d5715c HEAD@{6}: commit: Twig extension completed
97c9b87 HEAD@{7}: commit: Small error handling update
d600564 HEAD@{8}: commit: CreatedAt Tweak
7b7b2d8 HEAD@{9}: commit: Fixtures completed
72c1754 HEAD@{10}: commit: Files have been created
c974044 HEAD@{11}: checkout: moving from develop to entities
c974044 HEAD@{12}: checkout: moving from commands to develop
c974044 HEAD@{13}: checkout: moving from develop to commands
c974044 HEAD@{14}: checkout: moving from master to develop
c974044 HEAD@{15}: commit (initial): First commit
```
## Recover branch

Our last commit on deleted branch is on 6d7ad85 so we'll have to use it.

```sh
inanzzz-MBP:sport inanzzz$ git checkout -b relationships 6d7ad85
Switched to a new branch 'relationships'
```