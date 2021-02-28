---
title: How to Write Git Commit Messages
date: 2021-02-27
tags: [git, github, software engineering]
image: "git_commit.png"
---

A well-written git commit properly conveys what was done in the source code. As software engineering is a team project, being able to convey to others the intent of a commit is very important. 

In this article, I'll give a short guideline on how to write commit messages.

## Common Wisdom

Here is probably how you commit files.

```bash
$ git add .
$ git commit -m "A commit message"
$ git push origin master
```

This practice of making commits makes it seem that commit messages should be limited to single lines only. But commit messages can be well beyond a line and they are so quite often but go unnoticed. Beginners often overlook that there is a larger body of text in well-written commit messages. They are not to blame though as the title of a commit is what is visible in most places.

Let's say you fixed a typo. It would be committed with a message like-

```bash
$ git commit -m "Fix typo in README.md"
```

The above commit is ok. Fixing a typo needs no further explanation. However, let's say you fixed a bug. And you commit something like this-

```bash
git commit -m "Fix bug in addUser()"
```

This commit message is not quite sufficient. It requires further explanations like, "what was the bug?", "how was it solved?", "when did it occur?" In such scenarios, longer commit messages are required.

Here's how you should be writing long git commit messages.

```bash
$ git add .
$ git commit
# Your default text editor should open
# Write an explanation of all the changes you made in this commit
```

Typically a long git commit message has two parts- a subject and a body. In this article I'll explain in very brief how you should be writing longer commits like a pro.

## A. Writing the Subject

#### 1. Separate subject from body with a blank line

The first line is the most important part of a commit as it is treated as the subject/heading of the commit message and it summarizes the explanation of the rest of the body. A new line is to separate this subject from the body. 

#### 2. Use imperative mood 

Subjects should always be in the imperative mood. For example-

```text
- Fix database classes
- Add test cases
- Update dependency
- Revert to previous version
- Delete hard coded tokens
- Show recent entries first
- Deallocate memory
```

#### 3. Limit to 50 characters

To keep headings short and consistent, it is best to limit them to 50 characters.

If limiting to 50 characters proves difficult, it is a good indicator that this commit message needs to be broken down to several commits.

#### 4. Capitalize start, end without period

- Start the heading using a capital letter.
- Do not end the subject with a period (.) 

## B. Writing the body

#### 1. Start with summary

Write a summary of the commit that is a bit more exploratory than the title but shorter than the rest of the body.

#### 2. Use markdown

By using Markdown formatting in the message body, Github will format the text beautifully in its web interface, thus making it joyful for other developers to read commit messages.

#### 3. Wrap the body at 72 characters

Git never wraps text automatically. An unwrapped text will overflow screens and make it harder for developers to read messages. When writing, commit messages, wrap it at 72 characters so that Git renders everything within an 80 character limit.

#### Explain what and why, not how

How the code has changed is quite easy to observe. Git diffs and Github can neatly show committed code/pull requests. So, instead of explaining how the code was changed, it is more important to explain **what caused the change** or **why you made the change**. Try explaining things like-

- What effects does this change have?
- Why is this change necessary?
- How does this commit address the issue?

NOT-
- What are the changes?

#### Writing from different perspectives

A good commit message will convey the same message from the following 4 different perspectives and answer the questions listed appropriately.

1. From a user's perspective
    - What problem is being solved by the commit?
    - If it's a bug fixing commit, how was it discovered?
    - If it's a new feature, how will the user benefit?
1. From a manager’s perspective
    - What was the mistake in the application logic?
    - Why the change was made this way? What other ways were considered, but rejected?
    - What risks may occur when this change is applied?
1. From the code’s perspective
    - Explain code that may be hard to understand just by reading the source. Bullet points might be useful here.
    - Give evidence that the changes are correct. Show what test/data/activity proves that the change is ok.
1. From git’s perspective
    - Mention what commit SHA caused a bug to form
    - Add tokens like #1359 to external discussions. Github will look for these and automatically add cross-references


## Conclusion

Writing Longer commits may not be the easiest thing to do but taking the time to do it will certainly help others in the long run. Code does not always convey the intent of a change but a well-written commit can convey that intent to fellow developers which is much needed for proper maintenance of a project. Well-written commits can also document a project for new developers. So write long commits, write good commits. 

## References
1. [chris.beams.io/posts/git-commit](https://chris.beams.io/posts/git-commit/)
1. [medium.com/@joshuatauberer/write-joyous-git-commit-messages-2f98891114c4](https://medium.com/@joshuatauberer/write-joyous-git-commit-messages-2f98891114c4)
1. [medium.com/sourcelevel/7-git-best-practices-to-start-using-in-your-next-commit-f9dc54990e86](https://medium.com/sourcelevel/7-git-best-practices-to-start-using-in-your-next-commit-f9dc54990e86)
1. [Pro Git Book](https://git-scm.com/book/en/v2)