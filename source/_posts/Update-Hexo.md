---
title: Update Hexo
mathjax: true
toc: true
date: 2020-06-04 14:57:29
tags: [Hexo]
categories: daily
---

At first, all I want is making the [asset folder](https://hexo.io/docs/asset-folders.html) work, then I tried to update hexo and met a series of problem and got them solved.

<!--more-->

## Conflication of hexo-generator-feed and hexo 3

### Problem
The first problem I met is shown as following
```
Template render error: (unknown path) [Line 8, Column 25]
  Error: Unable to call `the return value of (posts["first"])["updated"]["toISOString"]`, which is undefined or falsey
```

### Solution

- I found a [issue](https://github.com/iissnan/theme-next-docs/issues/79) stating the same problem and [it was answered](https://github.com/iissnan/theme-next-docs/issues/79#issuecomment-287474959) that the plugin `hexo-generator-feed` and `hexo-generator-sitemap` is incompatible with `Hexo 3`

- [someone uninstalls these plugins to solve the problem](http://mixoo.cn/2020/02/08/hexo-tempalte-render-error/) which doesn't work for me as [maupassant-hexo](https://github.com/tufu9441/maupassant-hexo) requires `hexo-generator-feed`.

- As stated in the [`hexo-generator-feed` repo](https://github.com/hexojs/hexo-generator-feed): 
  - Hexo 4: 2.x
  - Hexo 3: 1.x
  - Hexo 2: 0.x
- While my version in `package.json` is `"hexo": "^3.2.0"` and `"hexo-generator-feed": "^1.2.2"`. I am guessing that update `hexo` and `hexo-generator-feed` might help solve the problem.
- And yes, when I have Hexo: 4.2.1 and hexo-generator-feed: 2.2.0, it is solved automatically.
- `npm rebuild node-sass --force`.

## Updating node and Hexo

### Updating Node.js
- Newer version of `node.js` is needed for updating Hexo.
- I forgot how I install my `node` originally. Here reinstalled it as follows
  1. `which node`
  2. `sudo rm -rf /usr/local/bin/node`
  3. `sudo rm -rf /usr/loca/lib/node_modules/npm/`
  4. `brew doctor`
  5. `brew cleanup --prune-prefix`
  6. `brew install node`
- [Uninstall node.js on OSX](https://stackoverflow.com/a/26919540/5798355).

### `Brew link node`
- Then I try to make the link use the command `brew link node` which shed me the error `Error: Could not symlink include/node/common.gypi`.
- The solution is [here](https://discourse.brew.sh/t/mac-osx-homebrew-error-could-not-symlink-include-node-common-gypi/4717)
  1. `sudo chown -R $(whoami) /usr/local/*`: change the owner of the files (root) to myself `$(whoami)`, otherwise, I couldn't rm `.gypi`, refer to [here](https://discourse.brew.sh/t/mac-osx-homebrew-error-could-not-symlink-include-node-common-gypi/4717/5) and [here](https://gist.github.com/rcugut/c7abd2a425bb65da3c61d8341cd4b02d)
  2. `rm '/usr/local/include/node/config.gypi'`
  3. `brew link --overwrite node`
- Then I met the [problem](https://stackoverflow.com/questions/47306169/npm-version-is-giving-errormodule-js538-throw-err-error-cannot-find-modul) when using `npm`, giving me the error `modeule.js:538 throw err;`
  - This is **solved** by reinstalling the node using homebrew.

### Update hexo
- modify the `package.json` and use the command `npm update` in the terminal.

## Downgrading node
- When I try to deploy `hexo d`, it gave me the error `TypeError [ERR_INVALID_ARG_TYPE]: The "mode" argument must be integer. Received an instance of Object`
- This is because the [version of `Node.js` is too high](https://zhuanlan.zhihu.com/p/136552969) and we need to downgrade it.
- [Downgrading through `brew`](https://medium.com/@georgeenathomas/3-step-process-to-downgrade-node-version-using-homebrew-bc0b0a72ae27) 
  1. `brew unlink node`
  2. `brew install node@12`
  3. `brew link node@12`: failed
  4. `brew link --overwrite node@12`

## About Node.js & NPM
### Node.js
- [Node.js wiki](https://en.wikipedia.org/wiki/Node.js)
> Node.js is an open-source, cross-platform, **JavaScript runtime environment** that executes JavaScript code **outside a web browser**. 

- [About Node.js](https://nodejs.org/en/about/), JavaScript runtime, asynchronous event-driven, concurrency etc.
- [tutorialspoint - introduction to Node.js](https://www.tutorialspoint.com/nodejs/nodejs_introduction.htm)
- [*Node.js is the New Black* by Louis Simoneau in July 2010](https://www.sitepoint.com/node-js-is-the-new-black/)

### npm
- node.js package manager.
- write packages needed into `package.json` and run `npm install` or `npm update`. All the packages are inside `node_modules`.
- An alternative: [yarn](https://yarnpkg.com/)
