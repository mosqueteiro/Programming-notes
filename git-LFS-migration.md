# GIT LFS MIGRATION
Migrating a repo to use `git lfs` (Large File Storage) is not a totally straight forward process and [Atlassians guide](https://confluence.atlassian.com/bitbucket/use-bfg-to-migrate-a-repo-to-git-lfs-834233484.html) was outdated and used a tools that currently (2019/09/03) has some issues for *LFS* migration. The collection of links contained herein should help guide through the process, especially the `git lfs migrate` tool!  

## Setup
Data is stored using `git lfs` (Large File Storage) and therefore `git lfs` will need to be installed prior to using these tools. See [Installing git lfs](https://help.github.com/en/articles/installing-git-large-file-storage).  

An entire copy of the repo should be pulled down  
```bash
$ git clone --mirror <repo address>
```  
and it is a good idea to save a backup of the repo before making any changes  
```bash
$ cd path/to/repo.git
$ git bundle create ../<repo name>.bundle --all
```
**_Note:_** This backup file can be cloned off of `git clone <name>.bundle`.

## Steps
### Cleaning
Make sure to start from the repo top directory  
```bash
$ cd path/to/repo.git
```  
For cleaning out the entire history of .zip and .csv files
```bash
# Convert all zip and csv files in your master branch
$ git lfs migrate import --include-ref=master --include="*.zip,*.csv"

# Convert all zip and csv files in every local branch
$ git lfs migrate import --everything --include="*.zip,*.csv"
```  
### Pushing back up to server
Since we started with a mirrored repo we can use a mirror push to rewrite what is on the server-side  
```bash
$ git push --mirror <repo address>
```
### Add file tracking
We should now be done with the repo mirror and can clone a working tree down  
```bash
$ cd ../
$ git clone <repo address>
```  
To add tracking for new files that will be added in the future which creates a `.gitattributes` file
```bash
$ git lfs track "*.zip"
$ git lfs track "*.csv"
```  
Then these changes need to be commited
```bash
$ git add .gitattribtues
$ git commit -m "Add .git attributes"
$ git push
```
_Note_: This will only add this file to the current branch  



## Git LFS migration links
* [Git LFS - large file storage | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/git-lfs)
* [Tutorial · git lfs migrate · GitHub](https://github.com/git-lfs/git-lfs/wiki/Tutorial)
* [git lfs migrate GitHub](https://github.com/git-lfs/git-lfs/blob/master/docs/man/git-lfs-migrate.1.ronn)
* [Use Git LFS with existing Bitbucket repositories - Atlassian Documentation](https://confluence.atlassian.com/bitbucket/use-git-lfs-with-existing-bitbucket-repositories-829078749.html)
* [Use Git LFS with Bitbucket - Atlassian Documentation](https://confluence.atlassian.com/bitbucket/use-git-lfs-with-bitbucket-828781636.html#UseGitLFSwithBitbucket-client)
* [Current limitations for Git LFS with Bitbucket - Atlassian Documentation](https://confluence.atlassian.com/bitbucket/current-limitations-for-git-lfs-with-bitbucket-828781638.html)


