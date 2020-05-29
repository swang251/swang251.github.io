---
title: Manage Your Own Package in Spacemacs
mathjax: true
toc: true
date: 2020-05-29 15:53:05
tags: [Emacs]
categories: Emacs
---
How to manage your own package or the one your forked in Spacemacs? The answer is the *layer*.
<!--more-->

## Create your layer
- `M-x` + `configuration-layer/create-layer`
- select `~/.spacemacs.d`
- The layer `<layerName>` is created with `packages.el` and/or `README.org` (depends on your choice).
- add your layer `<layerName>` into the variable `dotspacemacs-configuration-layers` in `~/.spacemacs.d/init.el`

## Manage your packages in `packages.el`
- `packages.el` contains a list of packages and their configuaration functions (init, post-init, etc...)
- Add your packages into `packages.el` following the grammar in the [documentation](https://develop.spacemacs.org/doc/LAYERS.html#packagesel)
  - Spacemacs supports different recipes to install a package. For managing our own package, we need to maintain it locally instead of remotely. This way, you would be able to debug and make sure it is working before your push it. 
  - For local multi-file package, one has to use
    ```
	(package-name :location (recipe :fetcher local))
	```
  - Initialize the package by adding 
  ```
  (defun layerName/init-packageName ()
      (use-package packageName
	   :init)
	   )
  ```
  - **IMPORTANT:** Multi-file local package is not supported yet byf the stable version Spacemaces. To make it work, one has to follow the [issues #8718](https://github.com/syl20bnr/spacemacs/pull/8718) and fix the corresponding files. Otherwise, clone the develop branch.
- Local packages should reside at `<layerName>/local/<packageName>`, git repository can be created within this folder.
- See [Configuration layers](https://develop.spacemacs.org/doc/DOCUMENTATION.html#configuration-layers) for more details




## Ref
- [Spacemacs Rocks Season 2](http://book.emacs-china.org/#orgheadline88)
- [Discussion in Emacs China](https://emacs-china.org/t/hack-package/2716)
