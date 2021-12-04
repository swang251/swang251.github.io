---
title: Matlab in Emacs
tags:
  - Emacs
  - Matlab
categories:
  - Emacs
  - Research Daily
mathjax: true
toc: true
date: 2021-12-03 15:10:47
---
Why programming and debugging Matlab in Emacs? There are two main reasons:

1. There are no Emacs emulators/keybindings available in Matlab on macOS, which makes Matlab programming less efficient.
2. One might need to program and debug Matlab scripts remotely.
<!--more-->

## Introduction
In order to program Matlab in Emacs, it must be able to 

- edit, including basic syntax, warning and error highlight, basic code completion, and
- debug, including running and debugging the scripts and basic command completion.

These [features are supported by the MATLAB mode for Emacs](http://matlab-emacs.sourceforge.net/faq.shtml), which provides the `matlab-mode`, `matlab-shell` and `mlint-mode`.

## Setup

1. Intall `matlab-mode` in Emacs, 
   - either from Melpa using package manager, or
   - clone the [repo](https://sourceforge.net/p/matlab-emacs/src/ci/master/tree/) to a local directory and load it manually in the `init.el`.
2. Add the following snippet into the `init.el`
  ``` lisp
  ;; associate .m file with the matlab-mode (major mode)
  (add-to-list 'auto-mode-alist '("\\.m$" . matlab-mode))
  
  ;; setup matlab-shell
  (setq matlab-shell-command "/Applications/MATLAB_R2021a.app/bin/matlab")
  (setq matlab-shell-command-switches (list "-nodesktop"))
  ```
  
## Usage
### Editing
- Open a `.m` file,
  - It should be in `matlab-mode` with syntax highlights
  - The `mlint-minor-mode` should be associated with `matlab-mode` and be turned on by default, with warning/error highlights
- `C-M-i` to complete symbol (call the function `matlab-complete-symbol`)
- `C-M-a` and `C-M-e` to jump to the beginning and end of a function ()
- Jump to the line with warning/error highlights and `M-x mlint-show-warning` to display the warning/error.
- `M-x matlab-shell-describe-command`

### Matlab-shell
- `M-x matlab-shell` to open the matlab shell, use it the same as the Command Window in a Matlab application.
- To run commands/scripts, one needs to go to the end of buffer `M->`, to the `>>`, and type the command/script name to run it.
- Press `<up>` will run the command `matlab-shell-previous-matching-input-from-input`, and shows previous run commands.
- `TAB` to complete commands
- Variable related commands
  - `workspace` to open the [workspace browser](https://www.mathworks.com/help/matlab/ref/workspace.html)
  - `who` to list all variables in workspace
  - `open <varName>` or `openvar <varName`  to open a variable in the variable editor

### Running and Debugging Scripts
- `Evaluate Section` run the commands `M-x matlab-shell-run-cell` (`C-M-return`)
- `Evaluate Selection`  select lines and run the commands `M-x matlab-shell-run-region` (`C-c C-r`)
- `matlab-emacs` use [GUD (Grand Unified Debugger library)](https://www.gnu.org/software/emacs/manual/html_node/emacs/Debuggers.html) to support for debugging
  - `C-x C-a C-b` (`gud-break()`) to set breakpoints
  - `C-x C-a C-v` (`gud-list-breakpoints()`) to list all breakpoints
  - `C-x C-a C-x` (`gud-remove()`) to remove breakpoints
- When the program is running, the script (`.m` file) will enter `matlab-shell-gud-minor-mode`, and becomes read-only. Use the following commands for debugging
  - `h`, **open help**
  - `b` **add breakpoint**, same as `C-x C-a C-b`
  - `x` **remove breakpoint**, same as `C-x C-a C-x`
  - `v` **list breakpoints**, same as `C-x C-a C-v`
  - `s` **step**, same as running `dbstep in` in the matlab shell
  - `n` **next**, same as running `dbstep` in the matlab shell
  - `f` **finish function**, same as running `dbstep out` in the matlab shell
  - `c` **continue**, same as running `dbcont` in the matlab shell
  - `q` **quit**, same as running `dbquit` in the matlab shell
- `gut-list-breakpoints` will open a buffer under `mlg-breakpoint-mode` listing all breakpoints

## Possible Problems
- The `mlint` doesn't show warnings/errors highlights
  - `M-: matlab-toggle-show-mlint-warnings` to toggle it on, or
  - add `(setq matlab-show-mlint-warnings t)` to the `init.el`
- `Error: no MLint program available` when trying to toggle on the `matlab-toggle-show-mlint-warnings` 
  ``` lisp
  ;; setup mlint for warnings and errors highlighting
  (add-to-list 'mlint-programs "/Applications/MATLAB_R2021a.app/bin/maci64/mlint") ;; add mlint program for macOS
  (add-to-list 'mlint-programs "/usr/local/MATLAB/R2021a/bin/glnxa64/mlint") ;; add mlint program for Linux
  ```


## References
- [MATLAB/Emacs integration project main page](http://matlab-emacs.sourceforge.net/)
- [MATLAB/Emacs FAQ](https://www.mathworks.com/matlabcentral/mlc-downloads/downloads/submissions/104/versions/3/previews/matlab-emacs-faq.html)
- [matlab-emacs git repo](https://sourceforge.net/p/matlab-emacs/src/ci/master/tree/)
- [Blog - Matlab Emacs Integration Is Back](https://blogs.mathworks.com/community/2009/09/14/matlab-emacs-integration-is-back/)
- [EmacsWiki - Matlab Mode](https://www.emacswiki.org/emacs/MatlabMode)
- [Matlab Documentation - Debugging and Analysis](https://www.mathworks.com/help/matlab/debugging-code.html)

