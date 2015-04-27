# Notes on Git for R and Bioconductor

## Git notes

* Delete local branch: `git branch -d <branch-name>`
* Delete remote branch: `git push origin :<branch-name>`


## Bioconductor-specific notes

### Bioconductor-to-GitHub bridge
* [Using the Bioconductor Git-SVN bridge](http://master.bioconductor.org/developers/how-to/git-svn/)
* [Git-SVN bridge web application](https://gitsvn.bioconductor.org/)

#### Setup bridge for Bioc devel
1. Create a GitHub repository, e.g. `http://github.com/<user>/<pkg>`

#### Setup bridge for Bioc release
1. Create a GitHub repository, e.g. `http://github.com/<user>/<pkg>-BioC-release`.  _Disable_ Wiki and Issue Tracker. Everyone should use the ones for the (above) Bioc devel GitHub repository.



