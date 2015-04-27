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

#### Local Bioc devel + release repository
Below describes how to setup a local Git repository that holds both the release and the devel versions of your Bioconductor package.  The two versions are contained in two different Git branches, namely:

* `master`: The package as currently on _Bioc devel_.
* `BioC-release`: The package as currently on _Bioc release_.

*IMPORTANT*: It is important to understand that these two branch should be considered "live", i.e. any commits and pushes to them will immediately be pushed to the corresponding SVN repositories over on the Bioconductor servers.

Setup:  

1. Add a 2nd remote repository named `release` pointing to the GitHub "BioC release" repository for you package
  - `git remote add release http://github.com/<user>/<pkg>-BioC-release`

2. Make the local `BioC-release` branch push to the `master` branch of this "release" repository:
  - `git push --force -u release BioC-release:master`


