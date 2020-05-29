---
title: Building a Personal Palabos Git Repository
mathjax: true
toc: true
date: 2019-12-17 01:05:22
tags: [Palabos, Git]
categories: [Palabos]
---
[Palabos](https://palabos.unige.ch/) just released a new version (v2.1r0) and pushed everything on [GitLab](https://gitlab.com/unigespc/palabos). This is something that all the Palabos community used to looking forward and makes it easier for the users to get official updates and contribute their own code. Personally, I would like to build my own Palabos version with in-house developed code while keeping updated from the official one. In this post, I am trying to talk about the Git workflow I use, which is mainly based on the [Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow) and the [Git Workflow](https://nvie.com/posts/a-successful-git-branching-model/).
![](/images/20191217/PalabosGitFlow.jpg)
<!--more-->
## Requirements
The workflow has to at least fulfill the following requirements.
- Allow private development: researchers might want to develop and test their own algorithms on Palabos. Some of the algorithms may not have been published yet. It is therefore reasonable to keep the repository private.
- Allow easy merge requests: This is about implementations of published algorithms or some complement functions/dataProcessors that should definitely be contributed to the official Palabos version.
- Allow updates from the UniGeSPC/Palabos: keep the personal repository up-to-date with the official one.
- Allow bug fixed both committed to the private and the official repositories.



## Forked Project
- Firstly, [fork](https://docs.gitlab.com/ee/gitlab-basics/fork-project.html) the project [UniGeSPC/palabos](https://gitlab.com/unigespc/palabos). After this, you could find the folked project under *Projects-->Your Projects*
- Go to your forked Palabos project. You can make it private by set the Project visibility to *private*. (Go to *Setting -->  General --> Visibility, project features, permissions --> Project visibility*)

## Branches
There are four kinds of branches:

### Master branch
The **master** branch is simply used to save a copy of the **UniGeSPC/palabos/master**. Whenever this is a new release/update from the upstream, it should be merged to the **master** branch which is then merged to the **develop** branch.

As our own Palabos project is forked from the **UniGeSPC/palabos**, when we first clone the GitLab repository, our **master** branch should be synchronized with the **UniGeSPC/palabos/master**.

In order to track the official Palabos project, we need to add the **UniGeSPC/palabos** as the upstream
```
$ git remote add upstream https://gitlab.com/unigespc/palabos.git
```
The upstream repository is shown when typing
```
$ git remote -v
```
As only the master branch of the upstream repository matters, I modified my *.git/config* so that whenever I call `git fetch`, it only fetches the **master** branch instead of all branches.
```
[remote "upstream"]
        url = https://gitlab.com/unigespc/palabos.git
        fetch = +refs/heads/master:refs/remotes/upstream/master
```

When there is a new release in the upstream, fetch it and merge it into **master**
```
$ git fetch upstream master
$ git checkout master
$ git merge upstream/master
$ git push origin master
```
The **master** branch is then merged to the **develop** branch that is introduced later.
```
$ git checkout develop
$ git merge --no-ff master
$ git push origin develop
```

### Develop branch
The **develop** branch is used for the development, including new features or algorithms. It is initially branched off from the **master** branch
```
$ git checkout -b develop master
```

However, it may never be merged back to **master**. Instead, whenever **master** gets an update from the upstream, it should be merged to **develop** branch.
```
$ git checkout develop
$ git merge --no-ff master
$ git push origin develop
```
Remember here we always use the flag `--no-ff` to avoid fast-forward merge.

> The --no-ff flag causes the merge to always create a new commit object, even if the merge could be performed with a fast-forward. This avoids losing information about the historical existence of a feature branch and groups together all commits that together added the feature. 

### Feature branch
The **feature** branch is used for both algorithm implementations and new functions/dataProcessors. It can be used for implementing both published and unpublished algorithms. The **feature** branch has a name convention **feature-***. Whenever starting a new **feature**, it should be branched off from either the **master** branch or the **develop** branch.

When you want to implement an algorithm that would be contributed to the upstream Palabos repository, you should branch off the **master** branch:
```
$ git checkout -b feature-DESCRIPTION master
```
Otherwise, you should branch off the **develop** branch:
```
$ git checkout -b feature-DESCRIPTION develop
```

When the development of a new feature is done and tested, it should be merged to the **develop** branch. 
```
$ git checkout develop
$ git merge --no-ff feature-DESCRIPTION
$ git push origin develop
```

If you want to [contribute](https://gitlab.com/unigespc/palabos/blob/master/CONTRIBUTING.md) this new feature to Palabos, you can create a [`merge request`](https://docs.gitlab.com/ee/gitlab-basics/add-merge-request.html).

You can also delete this branch once it is merged to both the **develop** branch and the official Palabos.
```
$ git branch -d feature-DESCRIPTION
```

### bugFix branch
**bugFix**  is used to fix bugs. It is suggested to open an issue for each bug your find. It could then be branched off from **develop**
```
$ git checkout -b bugFix-issueX develop
```
Once the bug is fixed, it should be merged back to the **develop** branch
```
$ git checkout develop
$ git merge --no-ff bugFix-issueX
$ git push origin develop
```
However, the Palabos Group might also fix the bug in the upstream branches if you don't create a `merge request` for your **bugFix** branch. If this happens, you might have to solve the conflict manually when you fetch **upstream/master** into the local **master** and then merged to the **develop**.

## Conclusion
Generally, this framework should work for most of our daily development and usage based on Palabos. My main doubt now is about the **master** branch. As it does nothing but saving a copy of the upstream, it seems reasonablbe to remove it. Everytime we see an new release from the upstream, the **upstream/master** could be directly merged in to the **develop** branch. However, the **master** branch is still kept for now to make the structure clearer.

Even though the workflow is not perfect, it allows us to maintain a customized Palabos while keeping the repository up-to-date with the upstream official Palabos. It is also easy to contribute to Palabos if you want. The flow diagram showed at the beginning is made based on [Vincent Driessen](https://nvie.com/posts/a-successful-git-branching-model/)'s template. Don't be hesitate to leave a message if you have any comments or suggestions. Thank you.

