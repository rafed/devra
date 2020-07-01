---
title: Useful terminal commands you are not using
date: 2020-06-27
tags: [terminal, linux]
draft: true
---

nano
htop
sensors (apt install lm-sensors)
free -h
df -h
du -h | sort -h
less
find
tar -xzvf
tar -cvf
time
crontab
sort < file.txt

convert +append input1.jpg input2.jpg output.jpg
convert -append input1.jpg input2.jpg output.jpg
convert -resize 50% input.png output.png
convert problem2.gif -shave 1x1 -bordercolor black -border 1 problem3.gif

This prints the file count per directory for the current directory level:
du -a | cut -d/ -f2 | sort | uniq -c | sort -nr

ctrl + x + e  for long terminal comands

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


https://dev.to/ko31/linux-commands-useful-when-performing-heavy-processing-2bdc?fbclid=IwAR0GxjASWcmSu3-WXYTJNiQDfQOsYOStyeErXLnvxu8otgjK57XAHaFbqP8

https://dev.to/javinpaul/10-simple-linux-tips-which-save-50-of-my-time-in-the-command-line-4moo?fbclid=IwAR3YodYtKgOnMQWCWoaWAOCKE7KU8CLXNd7ABZka4925pkQ-QshlgKzfzxY

https://dev.to/mateuszjarzyna/linux-s-commands-and-tricks-i-m-using-in-my-daily-job-as-a-developer-4cle?fbclid=IwAR0L9XP7gGvItWEwueSIxiPABqC5cvZKxPjbru5Qx4yh9cX7687MLNOYNzw

alias open='xdg-open &>/dev/null'
open ./some-file.html

alias clipboard="xclip -selection clipboard"
ls | clipboard

tools to use:
bat https://github.com/sharkdp/bat

http://www.linfo.org/wildcard.html


Linux Wildcards, Pipes, Redirects and Operators
> < |  >> <<


SSH
https://dev.to/djangotricks/things-i-want-to-remember-about-ssh-21el?fbclid=IwAR3Y8muaejqqSNiy-KnIUcVyz22mrHieCftVge2ujuMmqjhi_Hk0zWvzA6Q