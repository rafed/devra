---
title: Awesome Terminal Tricks to Boost Your Productivity
date: 2020-07-06
tags: [terminal, linux]
image: terminal.png
---

If you are glued to the terminal, you may want to use the following tricks to improve your productivity. These have been a life saver to me. If you're not a terminal user, these tricks will make you love the terminal again.

#### Contents:
- [Useful aliases](#useful-aliases)
- [Command editing hacks](#command-editing-hacks)
- [Running past commands](#running-past-commands)
- [Useful commands](#useful-commands)

## Useful aliases

<!-- Many confuse the usage of .bash_profile and .bashrc files. The difference
- .bash_profile is executed when bash is invoked as an interactive login shell (e.g. when SSHing)
- .bashrc is executed each time you open the terminal

It's best to **put aliases in .bashrc** because most .bash_profile configs also execute .bashrc when invoked. -->

Copy the lines starting with **alias** to your **~/.bashrc** file to enable them.

#### 1. Open a file in GUI mode
```bash
alias open='xdg-open &>/dev/null'
$ open home/        # opens home directory
```

#### 2. Copy output of a command

```bash
# Install xclip (apt-get install xclip)
alias c="xclip -selection clipboard"
$ ls | c            # copies output of ls (now you can paste)
```

#### 3. Show your public ip
```bash
alias myip='curl ifconfig.me'
$ myip              # outputs your ip
```

#### 4. Go back in directories
```bash
alias ..='cd ../'
alias ...='cd ../../'
alias ....='cd ../../../'
alias .....='cd ../../../../'
```

#### 5. Use bat instead of cat
```bash
alias cat=bat       # make sure bat is installed
$ cat myfile.txt    # apt-get install bat
```

#### 6. No need to type sudo everytime now when installing
```bash
alias apt-get='sudo apt-get'
```

#### 7. Start a http server
```bash
alias www='python3 -m http.server'
$ www               # starts server in the current directory
```

## Command editing hacks

<pre>
<kbd>Ctrl + x + e </kbd>     Edit big cmds in editor  
<kbd>Ctrl + a</kbd>          Go to beginning of cmd
<kbd>Ctrl + e</kbd>          Go to end of cmd  
<kbd>Ctrl + w</kbd>          Erase entire word  
<kbd>Ctrl + ←/→</kbd>        Move faster within the cmd
</pre>

## Running past commands

#### 1. Run the previously executed command
```bash
$ !!
$ sudo !! # previously executed command with sudo
```

#### 2. Run the last command starting with xxx
```bash
$ !xxx
```

#### 3. Reverse-i-search
```bash
# shows recent command based on the typed characters
$ Ctrl + r [now type chars]   
```

#### 4. Search by filtering entire search history
```bash
$ history | grep "xxx"        # searches for commands including xxx
```

## Useful commands

#### 1. Know when internet connection is up
```bash
$ ping 8.8.8.8 -a     # Makes periodic beeps when there is connectivity
```

#### 2. Show open ports
```bash
$ sudo lsof -ni
```

#### 3. Live read log files
```bash
tail -f /var/log/my-app/my-app.log | grep ERROR
```

#### 4. Simple image editing
```bash
# Must have imagemagick installed (apt-get install imagemagick)

# Append multiple images horizontally
convert +append input1.jpg input2.jpg output.jpg

# Append multiple images vertically
convert -append input1.jpg input2.jpg output.jpg

# Reize image
convert -resize 50% input.png output.png

# Add border to image
convert input.gif -shave 1x1 -bordercolor black -border 1 output.gif
```

### 5. Easily go to last directory
```bash
# Takes you to the previous directory you were in
cd -
```

<!-- Awesome Terminal Productivity
  https://github.com/chubin/cheat.sh
  https://github.com/tldr-pages/tldr
 -->
