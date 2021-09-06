---
title: Look How Google Writes Technical Documentations! (With Examples)
date: 2021-09-06
tags: [software engineering]
image: documentation.jpg
---

Writing software is hard. And writing documentation is harder. No wonder good documentations are hard to find.

But it shouldn't be this way.

Thankfully I stumbled upon [Google's technical document writing course](https://developers.google.com/tech-writing/overview). They formulated it based on their years of experience and numerous researches. It's a short read and should take no one more than 2 hours to complete.

This blog post was written to shorten and summarize the contents of that course. I can gurantee you have something to take away from this post. Enjoy!

## Table of contents
1. [Words](#1-words)
1. [Active voice](#2-active-voice)
1. [Clear sentences](#3-clear-sentences)
1. [Short sentences](#4-short-sentences)
1. [List and tables](#5-list-and-tables)
1. [Paragraphs](#6-paragraphs)
1. [Audience](#7-audience)
1. [Documents](#8-documents)
1. [Punctuation](#9-punctuation)

## 1. Words

Words are what documents are made of. Being able to use words appropriately can make quite the difference.
#### 1.1 Define new or unfamiliar terms

* Recognize terms that might be unfamiliar to some/all of your target audience. Once identified:
    1. Define the terms if not defined before.
    1. If already defined, link to an existing explanation


#### 1.2 Use terms consistently

* Use the same term consistently throughout a document. 
* Shorten repeating long words

Bad examples:

> * Kubernetes is an open-source platform for managing containerized workloads and services. K8s is being widely adopted by many companies.
> * Machine learning is a growing field. More and more companies are starting to hire machine learning engineers.

Good examples:

> * **Kubernetes** (or **K8s** for short) is an open-source platform for managing containerized workloads and services. K8s is being widely adopted by many companies.
> * **Machine learning** (or **ML** for short) is a growing field. More and more companies are starting to hire ML engineers.


#### 1.3 Use acronyms properly

On the initial use of an acronym 
* Spell out the full term, and then put the acronym in parentheses
* **Boldface** both the spelled-out version and the acronym
* Use the acronym from then onwards. Don't cycle between full the acronym and full form


Example:

> **Object Oriented Programming (OOP)** is a very popular programming paradigm. That is why OOP is taught in many programming boot camps.

#### 1.4 Disambiguate pronouns

These pronouns can cause confusion:

* it
* they, them, and their
* this, that

To make it less confusing:

* Use a pronoun only after introducing the noun
* Place the pronoun as close as possible to the referring noun. If more than five words separate your noun from your pronoun, repeat the noun instead of using the pronoun
* If you introduce a second noun between your noun and your pronoun, reuse your noun instead of using a pronoun

Bad examples:

> Python is interpreted, while C++ is compiled. It is extremely fast
> Grafana and Loki are similar to Loki and Kibana and they are growing rapidly
> Import may configure the app statically or dynamically. It can pose a security risk

## 2. Active voice

The majority of sentences should be in active voice. Because:

* Most readers mentally convert passive voice to active voice. So no need to add extra processing time to readers
* Passive voice obfuscates your ideas
* Some passive voice sentences omit an actor altogether, which forces the reader to guess the actor's identity.
* Active voice is usually shorter than passive

> Be bold—be active.

Bad examples:

> * The code was parsed by the compiler.
> * The product was tested by QA and deployed by the DevOps team.
> * The results were then evaluated.

Good examples:

> * The compiler parsed the code.
> * QA tested the product and DevOps team deployed it.
> * The researchers evaluated the results.

## 3. Clear sentences

#### 3.1 Choose strong verbs

These verbs are weak or generic and should be reduced:

* forms of be: is, are, am, was, were, etc.
* occur
* happen

Consider strengthening them and make them more engaging.

Bad examples:

> * The error **happens** when clicking the button.
> * The error message **occurs** when ...
> * The devs **are** very careful when editing the file

Good examples:

> * Clicking the button **generates** the error
> * The system **triggers** the error message when ...
> * The devs carefully edit the file.

#### 3.2 Reduce there is/there are

Bad examples:

> * There is a variable called ```weather``` that stores the current temperature.
> * There are two problems with Python you should know.
> * There is no guarantee that the updates will be received regularly.

Good examples:

> * The ```weather``` variable stores the current temperature.
> * You should know two problems about Python.
> * Clients might not receive the updates regularly.

#### 3.3 Minimize certain adjectives and adverbs 

Adjectives and adverbs tend to be loosely defined and can cause problems for technical readers. Omitting them might be preferable.

Bad examples:

> * The v2 compiler is blazingly faster than v1!

Good examples:

> * The v2 compiler is 200% faster than v1!

## 4. Short sentences

## 5. List and tables

#### 5.1 Choose the correct type of list

Lists are of three types:
* bulleted lists
* numbered lists 
* embedded lists

Use a **bulleted list** for unordered items; use a **numbered list** for ordered items. That means:
* If you rearrange the items in a bulleted list, the list's meaning does not change.
* If you rearrange the items in a numbered list, the list's meaning changes.

For example, the following bulleted list does change the list's meaning when reordered:
> The commonly used tools in Kali OS are:
> * Metasploit
> * Nmap
> * Burpsuite

The following list uses a numbered list because reordering them changes the meaning:
> Do the following to change server configuration:
> 1. Stop the server
> 1. Change env variables accordingly
> 1. Start the server

An embedded list contains items stuffed within a sentence. For example, the following sentence contains an embedded list with four items.

> The compiler reads the code, tokenizes the strings, creates AST and generates bytecode.

Generally, embedded lists are a bad idea. Try to convert them to ordered or unordered lists.

#### 5.2 Keep list items parallel

All items in a list should look as if they belong together.

Example of a nonparallel list:

> * C++
> * Python
> * Java
> * React

Unlike the others, React is a framework rather than a programming language.

#### 5.3 Start numbered list items with imperative verbs

An **imperative verb** sounds like a command. Like **start** or **stop**. The following example shows how imperative verbs should be used in ordered lists:

> 1. Download the app.
> 1. Register an account.
> 1. Make the payment.
> 1. Enjoy our services.

#### 5.4 Punctuate list items properly

If a list item is a sentence, use sentence capitalization and use punctuation. Otherwise, skip them.

Example when capitalization and punctuation are required:

> 1. Search for the configuration file.
> 1. Change the environment variables
> 1. Rerun the tests.

Example when they are not needed:

> Your responsibilities in this project include:
> * writing business code
> * run ansible scripts
> * handle servers
> * automate testing

#### 5.5 Create useful tables

Organized minds tend to love tables. Consider the following guidelines when making them:

* Label each column with a header.
* Avoid too much text in one cell. If a cell contains more than two sentences, consider refactoring it.
* Make each column parallel (i.e. should not be a mixture of more than one data type).

#### 5.6 Introduce each list and table

Introduce each list and table with a sentence that tells readers what they are all about. In other words, give the list or table context. For example:

> * The following list identifies key performance parameters:
> * Take the following steps to install the Frambus package:
> * The following table summarizes our product's features against our key competitors' features:


## 6. Paragraphs

#### 6.1 Write a great opening sentence

The opening sentence is the most important sentence of any paragraph. Because:
* It establishes the paragraph's central point.
* Busy readers focus on opening sentences and may skip over subsequent sentences. 

Consider the following paragraph:

> The Pythagorean Theorem states that the sum of the squares of both legs of a right triangle is equal to the square of the hypotenuse. The k-means clustering algorithm relies on the Pythagorean Theorem to measure distances. By contrast, the k-median clustering algorithm relies on the Manhattan Distance.

The opening sentence is defective because it seems like the Pythagorean Theorem will be discussed in the paragraph. But since it talks about clustering algorithms, a better opening sentence would be:

> Different clustering algorithms measure distances differently.

#### 6.2 Focus each paragraph on a single topic

* A paragraph should represent an independent unit of logic
* Restrict each paragraph to the current topic.
* Don't describe what will happen in a future topic or what happened in a past topic.
* When revising, **ruthlessly delete** (or move to another paragraph) any sentence that doesn't directly relate to the current topic.

#### 6.3 Don't make paragraphs too long or too short

For long paragraphs:

* Long paragraphs are visually intimidating and can be ignored by readers.
* Paragraphs containing 3 to 5 sentences are more welcoming to readers.
* Avoid paragraphs containing more than 7 sentences. 
* When revising, consider dividing very long paragraphs into two separate paragraphs.

For short paragraphs:

* Don't make paragraphs too short.
* If a document contains plenty of one-sentence paragraphs, your organization is faulty.
* Seek ways to combine those one-sentence paragraphs into cohesive multi-sentence paragraphs or possibly into lists.

#### 6.4 Answer what, why, and how

Good paragraphs answer the following three questions:

1. **What** are you trying to tell your reader?
2. **Why** is it important for the reader to know this?
3. **How** should the reader use this knowledge? Alternatively, how should the reader know your point to be true?

## 7. Audience

> good documentation = knowledge and skills your audience needs to do a task − your audience's current knowledge and skills

Therefore, to make good documentation you need to:
1. Define your audience.
1. Determine what your audience needs to learn.
1. Fit documentation to your audience.


#### 7.1 Define your audience

##### Identify potential audience roles

* software engineers
* students
* scientists

##### Then, make assumptions on what the target audience already knows:

* My target audience already knows Python.
* My target audience has not learned anything about machine learning.
* My target audience took linear algebra in university, but many members of the team need a refresher on matrix multiplication.

#### 7.2 Determine what your audience needs to learn

Write down a list of everything your target audience needs to learn to accomplish goals.

For example:

> After reading the documentation, the audience will know how to do the following tasks:
> * Use scikit-learn to build classical machine learning models
> * Use Tensorflow to build deep learning models

#### 7.3 Fit documentation to your audience

Write hocumentation that satisfies your audience's curiosity rather than your own. This is not always an easy task. However, there are a few things you could focus on:

* Match vocabulary to your audience or use simple words instead of difficult ones.
* Experts often suffer from the curse of knowledge. This means, their expert understanding of the topic ruins their explanations to newcomers. So try to write the document from a beginner's point of view.


## 8. Documents

A good document should be well organized and coherent. By focusing on the following points it can be made better.

* State the document's scope:
    * Define the scope of this document.
    * Additionally, define the topics that are not covered in the document that your audience might expect to be covered.
* State the audience- for which groups of people this document is applicable.
* Write for the audience. Keep in mind what their knowledge level is and what they expect to learn here.
* Break a topic into sections.

