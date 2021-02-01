---
title: Why Even Noobs Should Participate in CTFs
description: 
date: 2019-10-19
tags: [security]
image: "ctf.jpeg"
---

A few days back Facebook held their first-ever CTF and Google also held theirs a few days later. Although I occasionally goof around with CTFs, I'm no expert at it. Despite this, I decided to take an attempt. I was skeptical at first but it turned out to be an awesome experience.

In case you don't know what a CTF (capture the flag) is, it's almost like a treasure hunt where you have to find a treasure by exploiting security loopholes. The treasures are usually strings and images. You can discover them by exploring a given program/app and exploiting/decrypting stuff.

Although I couldn't solve most of the problems, as a software engineer and a student I did have a lot to take away. Some of the CTFs were based on cutting edge technology that Facebook and Google themselves use and maintain. Here's some new tech that I encountered.

## Apache Thrift

The name of the challenge was "homework_assignment_1337" from Facebook. It involved developing a Thrift client based on a provided .thrift file. But what the heck is Thrift?

In the past SOAP was the only way to go for RPCs (Remote Procedure Calls). Soon we moved to REST, gRPC and other protocols. The new kid on the block for RPCs is Thrift. It is basically a software framework for scalable cross-language services development.  It can work efficiently and seamlessly between C++, Java, Python, PHP, Ruby, Node, C#, and many other languages. This project is maintained and used by Facebook. I'm surely going to use it for my next distributed systems project.

I almost solved this problem. But almost doesn't really count, does it...

## Osquery

Another challenge from Facebook was "osquery_game". It involved playing a game (farming game) by running SQL queries on osquery. But what the heck is osquery?

If you're a person who needs to monitor your pc/server performance for your deployed app, osquery might be the perfect tool for you. Traditionally you would need to run scripts or bash commands to see different stats of your server. With osquery you can simply write SQL to see device status. Query your devices just like a database! This can be incredibly powerful. And the best thing, it works on all platforms- Linux, Windows, and Mac.

This challenge was too hard for me. But at least I got to play with osquery.

## Go

This problem was from Google and it's called "Doomed to Repeat It". It's a memory game (like Mahjong) that has several constraints that make it impossible for any human to solve normally. The problem was made with Js and Go. What the heck is Go?

Go (also known as Golang) is a programming language developed by Google for systems programming.  It is an awesome language because of its built-in concurrency and speed. Try it out if you're into building scalable backends. As I did work with Go before, it was not new for me. I still couldn't solve the problem though.

There you go! Three awesome techs that you probably haven't heard of. The challenges I mentioned above, are the ones I couldn't solve. But I did learn about new tech and so can you. CTFs are designed this way so that you continuously have to learn new stuff. I don't know how well I can solve the CTFs next year but I'm still gonna try and so should you.
