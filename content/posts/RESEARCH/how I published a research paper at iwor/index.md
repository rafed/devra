---
title: How I Accidentally Published a Research Paper at IWOR (ICSE)
date: 2019-12-08
tags: [research]
image: "iwor.png"
---

In our final semester of university, we had a course called "Software Metrics." Ths study of software metrics aims at measuring the properties of software. I didn't like this course very much. It was theoretical and a bit boring. I'm usually fond of more practical stuff.

In most of our courses, we have to complete a project by the end of the semester. For the software metrics course, we were to build a tool that shows several known metrics of a Java program. Also, we had to extend the tool to add new features and make a publication out of it.

Now, this was ridiculous. As a beginner who just heard the term software metric yesterday (and hated it as well 😛), it was quite impossible to propose a new metric tool and publish a paper on it (at least for me). Also, in terms of software metrics, Java is probably the most studied languages so it is very difficult to do something new. We did take some attempt initially but eventually realized that it's not really possible in the time span of a semester.

At that time I was really into Go (Google's programming language). I enjoyed its speed of execution and concurrency features (goroutines). Go is an amazing language for writing system programs/backends. I built some simple APIs with it. It's then when my mind clicked, why not propose a metric tool for Go programs? Go is a relatively new language and no work on metrics of Go programs has been done yet.

We requested our sir, that we wanted to work on Go metrics. To our favor, he gladly allowed us.

So we made a tool called GodExpo. It finds God structs in Go programs. It's nothing complicated, pretty simple stuff. We just brought the concept of "god classes" in Go as "god structs" (since Go does not have classes).

We wrote a short tool paper explaining our tool. We planned to submit the paper to a good conference, get rejected, and get feedback on what needs to be improved. And then finally submit it to an average ranked conference.

So we submitted our paper to IWOR (International Workshop on Refactoring). It's a good workshop being co-located with ICSE (International Conference on Software Engineering). ICSE is the highest ranked conference in software engineering (A* star ranked). We didn't think that we'd get an acceptance and patiently waited for the review in our rejection letter.

Boy, I'm glad we were wrong about that. Our paper surprisingly got accepted! And that's how I got a publication at IWOR.

You can find the paper at [dl.acm.org/citation.cfm?id=3340645](https://dl.acm.org/citation.cfm?id=3340645). The tool can be found on Github at [github.com/rafed123/GodExpo](https://github.com/rafed/GodExpo). Make sure to give it a star. 😃
