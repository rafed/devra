---
title: Useful Terminal Commands You Need to Use NOW!
date: 2021-03-30
tags: [terminal, linux]
image: htop.png
---

Linux is loaded with different commands. In this article, I'm just listing the ones that I frequently use all the time.

## 1. Monitor your PC

#### Task manager equivalent for Linux
```bash
# sudo apt install htop
$ htop
```

#### Monitor system temperature
```bash
# sudo apt install lm-sensors
$ sensors
```

#### Check ram usage
```bash
$ free -h
```

#### Check system specs
```bash
$ lscpu 
$ cat /proc/cpuinfo
```

#### Check disk usage
```bash
$ df -h
```

#### Check file space usage of current directory
```bash
$ du -sh *
$ du -h | sort -h

#### Print the file count per directory for the current directory level
$ du -a | cut -d/ -f2 | sort | uniq -c | sort -nr
```

#### Check if anyone is logged in
```bash
$ who
```

## 2. File Operations

#### Edit a file in the terminal
```bash
$ nano file.txt
```

#### Scroll through a file
```bash
$ less file.txt
# Press 'q' to quit
```

#### Clear contents in a fille
```bash
$ cat /dev/null > file.txt 
```

#### Rename a file to add extension easily
```bash
# renames file.md -> file.md.backup
mv /folder/file.md{,.backup}
```

#### Print a file in reverse
```bash
$ tac file.txt
```

#### Tar compression decompression
```bash
# Compress a file
$ tar -czvf archive.tar.gz /path/to/directory-or-file

# Extract a file
$ tar -xzvf archive.tar.gz

# z means gzip
# To use bzip2 replace 'z' with 'j'
# gzip is faster but bzip2 makes smaller archives
```

#### Sort a file
```bash
$ sort < file.txt
```

#### Search for files
```bash
$ find . -name "*.mp3"
$ find . -type f -size +100M
```

#### Live read a system log
```bash
$ tail -f /var/log/app.log 
$ tail -f /var/log/app.log | grep ERROR
```

## 3. Command execution

#### Measure time of execution of a program
```bash
$ time anyprogram
```

#### Cron jobs to execute commands periodically
```bash
$ crontab -e
```
Get help from [crontab.guru](https://crontab.guru/) for making crons easily.

## 4. Networking

#### Get websites listed in a file
```bash
$ curl $(cat websites.txt)
# or (another form of command substitution)
$ curl `cat websites.txt`
```

#### Check occupied ports
```bash
$ lsof -i
$ lsof -ni
```

#### Port forward remote machine to your machine

```bash
$ ssh -L2000:localhost:1313 root@10.100.101.45
# ssh -L{local_port}:localhost:{remote_port} user@remote.ip
```

## 5. Wildcards, and Redirects 

#### Remove all files except .html
```bash
rm -r !(*.html)
```

#### Redirecting

Just remember- 
* 0 - stdin, the standard input stream.
* 1 - stdout, the standard output stream.
* 2 - stderr, the standard error stream

##### Redirect stderr to file
```bash
command 2> file
```

##### Stderr and stdout to different files
```bash
command 2> error.txt 1> output.txt
```

##### Suppress error messages
```bash
command 2> /dev/null
```

##### Redirect stderr to stdout
```bash
command > file 2>&1
```

#### For wildcards, check the following

1. [Linux wildcards](http://www.linfo.org/wildcard.html)

## Conclusion

That seems to be most of the Linux commands that I use all the time. If you have more suggestions to add, comment down below. Check out my other article where I show [Terminal tricks to boost your productivity](/devra/posts/terminal/awesome-terminal-tricks-to-boost-your-productivity/).