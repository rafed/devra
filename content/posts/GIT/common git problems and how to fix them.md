---
title: Common Git Problems and How to Fix Them
date: 2020-06-27
tags: [git, github]
draft: true
---

### Git
https://dev.to/bellawoo/how-to-fix-a-typo-after-you-ve-already-pushed-your-commit-342l
basics of git and github { //// bare minimum git commands to know
    Revert - You want to be able to confidently undo changes that break your code.
    Track changes - You want to be able to figure out what was necessary to implement a feature, or how various code is related to other code.   Mostly, you want to know why somebody chose to write a particular piece of code.
    
    https://dev.to/andydangerous/how-i-git
    https://github.com/k88hudson/git-flight-rules
    https://dev.to/murkrage/five-git-commands-i-started-using-that-might-be-helpful-to-you-536e
}

git reset (unstage accidentally staged files)
add upstream when cloned repository is behind commits of main branch

# set remote url when changed
git remote set-url origin new.git.url/here



$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com

$ git config --global core.editor nano