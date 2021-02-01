---
title: Useful Terminal Commands You are not Using
date: 2020-06-27
tags: [terminal, linux]
iamge: htop.png
draft: true
---

nano
htop
sensors (apt install lm-sensors)
free -h
df -h
du -h | sort -h
du -sh *
less
find
tar -xzvf
tar -cvf
time
crontab
sort < file.txt
nice

This prints the file count per directory for the current directory level:
du -a | cut -d/ -f2 | sort | uniq -c | sort -nr

pushd popd dirs -c
dirs

?? *.[mM]p3


find . -type f -size +100M
find . - name "*.mp3"

cat /dev/null > file.txt  [ to clear contents]
tac

command subsitution $(which curl) or `which curl`  (backticks)

curl $(cat websites.txt)

rm -r !(*.html)

tools to use:
bat https://github.com/sharkdp/bat

http://www.linfo.org/wildcard.html


Linux Wildcards, Pipes, Redirects and Operators
> < |  >> <<

