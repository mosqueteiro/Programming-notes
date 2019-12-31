# git version controls notes  

[A successful git branching model](https://nvie.com/posts/a-successful-git-branching-model/) is heavily used.

## Contents  

* [old feature > newer master](#getting-a-feature-branch-up-to-speed-with-master)
* [References](#references)  


## Getting a feature branch up to speed with master  

A `feature` was developed but not immediately merged into `master`. `master` has since had commits added to it. To prepare to merge the `feature` into `master` we need to get the `feature` up to speed with the `master` and check for merge conflicts.  

From [stackoverflow:](https://stackoverflow.com/a/5309051/4794025)
> Say your bug fix branch is called bugfix and you want to merge it into master:
>
>```bash
>git checkout master
>git merge --squash bugfix
>git commit
>```
>
>This will take all the commits from the bugfix branch, squash them into 1 commit, and merge it with your master branch.
>
>Explanation:
>
>```bash
>git checkout master
>```
>
>Switches to your master branch.
>
>```bash
>git merge --squash bugfix
>```
>
>Takes all the commits from the bugfix branch and merges it with your current branch.
>
>```bash
>git commit
>```
>
>Creates a single commit from the merged changes.
>
>Omitting the `-m` parameter lets you modify a draft commit message containing every message from your squashed commits before finalizing your commit.
>
>>In case merge conflicts happen and you resolve these conflicts, git commit will no longer show the useful commit message containing all commit messages you squashed. In that case, try git commit --file .git/SQUASH_MSG (via [stackoverflow.com/a/11230783/923560](http://stackoverflow.com/a/11230783/923560)).

## References  

* [A successful git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
