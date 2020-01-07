# Portworx Documentation

[![Travis branch](https://img.shields.io/travis/portworx/pxdocs/master.svg)](https://travis-ci.org/portworx/pxdocs)

A [hugo](https://gohugo.io/) implementation of the Portworx documentation.

## Contributing to the docs

* Click the Fork button in the upper-right area of the screen to create a copy of this repository in your GitHub account. This copy is called a fork. 
* Make any changes you want in your fork, and when you are ready to send those changes, go to your fork and create a new pull request.
* Once your pull request is created, assign the PR to a reviewer who is the SME (subject matter expert). As the owner of the pull request, it is your responsibility to modify your pull request to address the feedback that has been provided to you by the reviewer.

Below are useful pages that will be useful if you are contributing to the docs.

* [Recommended git workflow for contributing](GIT_WORKFLOW.md)
* [Tip and tricks for editing content](TIPS_AND_TRICKS.md)
* [Documentation on search functionality](SEARCH.md)
* Recommended editors
    * [Visual Code](https://code.visualstudio.com/)
    * [Atom](https://atom.io/)

## Versioning and Branching

Following is a table that maps each version in the dropdown to the git branch in the repository.

| Git branch | Portworx version                    |
|------------|-------------------------------------|
| master     | 2.4.x                               |
| 2.3        | 2.3.x                               |
| 2.2        | 2.2.x                               |
| 2.1        | 2.1.x                               |
| 2.0.3      | 2.0.3.x                             |
| 2.0        | 2.0.1, 2.0.2                        |
| 1.7        | 1.7.x                               |

[Documentation on version dropdown](VERSIONS.md) has details on making changes to version branches.

## Running the site locally

To develop the docs site locally - first ensure you have [docker](https://docs.docker.com/install/) installed.

Pull in the theme from the [pxdocs-tooling](https://github.com/portworx/pxdocs-tooling) repo using below command:

```bash
make update-theme
```

Now, launch the website locally using:

```bash
make develop
```

You can then view the site in your browser at [http://localhost:1313](http://localhost:1313).  As you edit content in the `content` folder - the browser will refresh automatically as you save files.

## Updating the theme

It's important to make sure the theme the docs site uses is up to date.  To do this:

```bash
make update-theme
```

This will pull in the latest content from [pxdocs-tooling](https://github.com/portworx/pxdocs-tooling) - make sure you `git commit` once you have updated the theme.

Make sure you update the theme for each of the version branches if the theme changes.

If you want to make changes to the templates or CSS - these files live in the `layouts` and `static` folder of the [pxdocs-tooling](https://github.com/portworx/pxdocs-tooling) repo.  Make the changes there and then re-update each of the version branches.

### Updating the theme to a custom branch

Production build should only use the master branch of the [pxdocs-tooling](https://github.com/portworx/pxdocs-tooling) repo. For testing private changes, you can use the following:

```bash
TOOLING_BRANCH=my-branch make update-theme
```

This will update the submodule for tooling/theme to the given "my-branch".

### Resetting the theme

```bash
make reset-theme
```


## Deployment to production

Deployment of your changes is handled by Travis upon a git push to the git repo.  Once you have made changes and viewed them locally - a `git push` of the version branch you are working on will result in the content being deployed into production.
