---
title: Top free security practice website for free
date: 2020-07-18
tags: [security]
image: metasploitable.png
draft: true
---

tryhackme
vulnhub
picoctf
hackthebox
overthewire
https://github.com/vulhub/vulhub

The best way to learn security concepts is by doing it. But how to do it if you don't know it? These vulnerable apps will make you learn and do it! 

## 1. DVWA

[Damn Vulnerable Web App (DVWA)](http://www.dvwa.co.uk/) is a **PHP/MySQL** web application that is damn vulnerable. 

The app is divided into sections for different types of vulnerabilities. The best thing about DVWA is it has **lessons/guidelines** on how to exploit a vulnerability.

## 2. Webgoat

[WebGoat](https://owasp.org/www-project-webgoat/) is a deliberately insecure application that allows you to test vulnerabilities commonly found in **Java-based** applications that use common and popular open source components.

Like DVWA this also has tutorials for each vulnerability.

## 3. Juice Shop

OWASP [Juice Shop](https://owasp.org/www-project-juice-shop/) is probably the most modern and sophisticated insecure web application! It is written entirely in **JavaScript (Node.js, Express, Angular)**. 

Juice shop also has tutorials for several of the easy challenges.

## 4. Metasploitable

Metasploitable is a vulnerable virtual machine intended for practicing taking over machines. Intended to be practiced with metasploit- the ultimate vulnerability exploitation tool, this vulnerable VM is one of the most enjoyable ones to play with. It has three versions:
1. [Metasploitable](https://www.vulnhub.com/entry/metasploitable-1,28/): Released in 2010, this one is quite old. A lot of the vulnerabilities are not valid anymore.
2. [Metasploitable 2](https://www.vulnhub.com/entry/metasploitable-2,29/): Released in 2012, this one is more beefed up with vulnerabilities.
3. [Metasploitable 3](https://github.com/rapid7/metasploitable3): This one is the latest version and the one you should be focusing on.

The difference between versions 2 and 3 is that in metasploitable 3, you will also get to practice on windows environments. Metasploitable 1 and 2 are only Linux based.

## 5. Security Shepherd

The [Security Shepherd](https://github.com/OWASP/SecurityShepherd) Project is a web and mobile application security training platform. This is the only app in this list that can provide a flavor of mobile app pen-testing.

The above apps are the best to get started with and practice penetration testing. However, there are some lesser-known apps that you can also try out to further improve your skills.

## 6. bWAPP

[Buggy web app (bWAPP)](http://www.itsecgames.com/) is also **PHP/MySQL** web app. It has over 100 vulnerabilities fo you to test.

## 7. DVNA

[Damn Vulnerable Node Application](https://github.com/appsecco/dvna) is a lesser-known vulnerable web app. Do this only after you have done Juice Shop.


## Bonus tip

Installing the vulnerable applications can be painful. It requires setting up multiple environments such as:
- Apache server
- PHP
- MySQL
- And other dependencies...

Not to mention, version conflicts is quite common. It could cause conflicts and break your environment.

You don't want this hassle. There's an easier way. Just use docker.

{{<highlight bash>}}
$ sudo apt-get install docker.io
{{</highlight>}}

And then just pull the image you want to use and run it. No need to install dependencies separately. This is way more convenient.

{{<highlight bash>}}
## 1. For DVWA
docker run --rm -it -p 80:80 vulnerables/web-dvwa

## 2. For Webgoat
docker pull webgoat/webgoat-8.0
docker run -p 8080:8080 -t webgoat/webgoat-8.0

## 3. For Juice shop
docker pull bkimminich/juice-shop
Run docker run --rm -p 3000:3000 bkimminich/juice-shop

## 4. Metasploitable is a VM. 
## DOwnload the VM and use it with virtual box.

## 5. For Security shepherd
docker pull owasp/security-shepherd

## 6. For bWAPP
docker run -d -p 80:80 raesene/bwapp

## 7. For DVNA
docker run --name dvna -p 9090:9090 -d appsecco/dvna:sqlite
{{</highlight>}}