# Notes on Git for R and Bioconductor

## Git notes

* Delete local branch: `git branch -d <branch-name>`
* Delete remote branch: `git push origin :<branch-name>`


## Bioconductor-specific notes

### Bioconductor-to-GitHub bridge
In this part it is described how to setup _one local Git repository_ that holds _two branches_, `master`(*) and `release`, that are "hot-linked" to the _"release"_ and the _"devel"_ versions of a Bioconductor package, respectively.  The hot-linking is done via two separate GitHub repositories that each are "bridged" to the Bioconductor Subversion repositories via the Bioconductor-to-GitHub bridge web service.  Here is an overview:

* Local `master` branch <=> GitHub "devel" repository (`master` branch) <=> Bioconductor Subversion "devel" repository
* Local `release` branch <=> GitHub "release" repository (`master` branch) <=> Bioconductor Subversion "release" repository

The end result is such that whenever commits to the `master` branch are pushed, the updates are immediately committed to the Bioconductor Subversion repository that holds the "devel" version of the package.  Any updates before 4:20pm Seattle time will checked over night, and the results and the updated package will be available before noon the next day.  This hot-linking is bi-directional, meaning that any commits to the Bioconductor Subversion repository will immediately be pushed to the GitHub repository via the bridge.

Similarly, whenever commits to the `BioC-release` branch are pushed, the "release" version of the package will be forwarded and eventually be built on the Bioconductor side.  Also this hot-link is bi-directional.

(*) Ideally we would call the `master` branch `devel` to reflect the fact that it is connected to the BioC "devel" package version, but the Bioconductor-to-GitHub bridge requires it to be named `master`.




* [Using the Bioconductor Git-SVN bridge](http://master.bioconductor.org/developers/how-to/git-svn/)
* [Git-SVN bridge web application](https://gitsvn.bioconductor.org/)

Subversion repositioryThe two versions are contained in two different Git branches, namely:

master: The package as currently on Bioc devel.
BioC-release: The package as currently on Bioc release.
IMPORTANT: It is important to understand that these two branch should be considered "live", i.e. any commits and pushes to them will immediately be pushed to the corresponding SVN repositories over on the Bioconductor servers.

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


