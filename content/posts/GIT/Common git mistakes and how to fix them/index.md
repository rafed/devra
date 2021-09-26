---
title: Common Git Mistakes and How to Fix them
date: 2021-06-24
tags: [git, github]
image: mistake.jpg
# draft: true
---

<!-- * You want to be able to confidently undo changes that break your cod
* Track changes - You want to be able to figure out what was necessary to implement a feature, or how various code is related to other code.   Mostly, you want to know why somebody chose to write a particular piece of code. -->

What's the worst thing you can do at your day job as a software developer?

Mess up the git project tree, that's for sure.

To err is human. But surely, nobody wants to be "the guy" who messed it up. So in this article, I'm going to show you the common mistakes everyone makes in git and how you can avoid/fix them (so that you don't have to be "the guy" who messes up stuff).

#### 0. Configure git after fresh install

Let's say you have a fresh git installation and is now about to make your first commit. But then git says 

```bash
Please tell me who you are
```

It's because, when you make a commit, git adds a name and an email to the commit so that others can know who made these changes. Let's configure the global name and email.

```bash
$ git config --global user.email johndoe@example.com
$ git config --global user.name "John Doe"
```

##### Bonus

The above commands set the global name and email. That means, for any repository you work in, the user and email always stay the same. If you want to set different names/emails for different repositories, go to the root of that repo and run the above commands again without the "--global" part.

```bash
# Inside a git repo
$ git config user.email dohnjoe@example.com
$ git config user.name "Dohn Joe"
```

#### 1. Update a commit message

Oops, you have a typo in your commit message. 

```bash
$ git commit --amend -m "New commit message"
```

#### 2. Update a file in a commit

Oops, you committed a random _print()_ statement and need to remove that. Make your changes accordingly, and

```bash
$ git add .
$ git commit --amend --no-edit # --no-edit for not changing commit message
```

_Don't amend pushed commits._

#### 3. Unmodify a modified file

Maybe you started modifying a file, but now want to unmodify it and get it back to its original form. Then run

```bash
$ git checkout -- filename
$ git checkout -- .  # To umodify the entire folder
```

_Don't amend pushed commits._

#### 4. Undo local commits

Oops, you have made commits but now want to undo them and go back to previous states. 

```bash
# Undo the last three commits, KEEP CHANGES
$ git reset HEAD~3

# Undo the last three commits, DISCARD CHANGES
$ git reset --hard HEAD~3
```

#### 5. Committed to a wrong branch

Oops, you were supposed to commit to a _new branch_ but committed to _master_. No problem.

```bash
$ git branch new-branch    # create the new branch to work with
$ git reset HEAD~ --hard   # reset the main branch to the previous commit
$ git checkout new-branch  # finally switch to the new branch
```

Avoid this mistake by making the habit of creating a new branch whenever you are implementing a new feature (even if they are going to be discarded later).

#### 6. Committed files that should have been ignored

Oops, you committed some files that should have been ignored (such as .env, exe). You add .gitignores for those but the files are still in the git tree. No problem, we can remove them.

```bash
# First, add files to be ignored in .gitignore
$ git rm -r --path/to/file .  
```

Or, if the number of files are too many

```bash
# First, add files to be ignored in .gitignore
$ git rm -r --cached .  # remove all files from git
$ git add .             # re-add all files
# Then, commit as usual
```

#### 7. Added Commits previously that needs to be removed (Repo NOT PUSHED to remote)

Let's say you made the following commits.

```bash
925ed76 commit 5
1ef488d commit 4
89c6e05 commit 3
8efbd1c commit 2
02baddf Commit 1
```

But now you have realized that changes made in commit 3 were a mistake and it needs to be removed.

The solution shown below will only work for repos not pushed to the remote. Run-

```bash
$ git rebase -i HEAD~3
```

This command will open an editor with the past 3 commits from HEAD so that you can pick or drop a commit. For example, the above would show something like this in a text editor-

```bash
pick 925ed76 commit 5
pick 1ef488d commit 4
pick 89c6e05 commit 3
```

Since we want to delete commit 3, remove that line and close the editor. That commit will be undone.

In some cases, merge conflicts may occur. In case they occur, resolve the conflicts and run-

```bash
4 git rebase --continue
```

#### 8. Added Commits previously that needs to be removed (Repo PUSHED to remote)

The solution in point 7 works when the repo is not pushed to the remote. What if the repo has been pushed and we want to remove past commits?

To solve this we need to use _git revert_. The _git rebase_ command shown previously modified the commit history to solve the issue. But this cannot be done now as the repo is pushed to the remote. The remote will reject the push as the commit tree will not match. A force push will work, but that will mess up the commit tree of other contributors to the project.

A _git revert_ adds a new commit that undoes changes made in a past commit. To revert, run-

```bash
$ git revert 1ab241 ## Hash of the commit to be undone
```

Then resolve conflict, merge and push. Voila!

