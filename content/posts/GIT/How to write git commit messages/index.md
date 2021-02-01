---
title: How to Write Git Commit Messages
date: 2020-07-27
tags: [git, github, software engineering]
image: "git commit.png"
draft: true
---

A well-written git commit properly conveys what was done in the source code. As software engineering is a team project, being able to convey others the intent of a commit is very important. 

In this guide, I'll just give a basic intro on how you should write commit messages.

#### 1. Common Wisdom

Here is probably how you commit files.

{{<highlight bash>}}
$ git add .
$ git commit -m "A commit message"
$ git push origin master
{{</highlight>}}


#### Separate subject from body with a blank line
#### Limit the subject line to 50 characters
#### Capitalize the subject line
#### Do not end the subject line with a period
#### Use the imperative mood in the subject line
#### Wrap the body at 72 characters
#### Use the body to explain what and why vs. how

Why is this change necessary?
How does this commit address the issue?
What effects does this change have?

Well-written commits in repositories will also attract more open source contributions.


https://medium.com/sourcelevel/7-git-best-practices-to-start-using-in-your-next-commit-f9dc54990e86
