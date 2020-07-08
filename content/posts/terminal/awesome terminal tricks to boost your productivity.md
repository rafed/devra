---
title: Awesome terminal tricks to boost your productivity
date: 2020-07-06
tags: [terminal, linux]
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

Copy the lines starting with **alias** to your ~/.bashrc file to enable them.

{{<highlight bash>}}
# 1. Open a file in GUI mode
alias open='xdg-open &>/dev/null'
$ open home/        # opens home directory

# 2. Copy output of a command
# Install xclip (apt-get install xclip)
alias c="xclip -selection clipboard"
$ ls | c            # copies output of ls (now you can paste)

# 3. Show your public ip
alias myip='curl ifconfig.me'
$ myip              # outputs your ip

# 4. Go back in directories
alias ..='cd ..'
alias ...='cd ../../../'
alias ....='cd ../../../../'
alias .....='cd ../../../../../'

# 5. Use bat instead of cat
alias cat=bat       # make sure bat is installed
$ cat myfile.txt    # apt-get install bat

# 6. No need to type sudo everytime now when installing
alias apt-get='sudo apt-get'

# 7. Start a http server
alias www='python3 -m http.server'
$ www               # starts server in the current directory
{{</highlight>}}

## Command editing hacks

<pre>
<kbd>Ctrl + x + e </kbd>     Edit big cmds in editor  
<kbd>Ctrl + a</kbd>          Go to beginning of cmd
<kbd>Ctrl + e</kbd>          Go to end of cmd  
<kbd>Ctrl + w</kbd>          Erase entire word  
<kbd>Ctrl + ←/→</kbd>        Move faster within the cmd
</pre>

## Running past commands

{{<highlight bash>}}

# Run the last exectued command
$ sudo !!

# Run the last command starting with xxx
$ !xxx

# Reverse-i-search
$ Ctrl + r [now type chars]   # shows recent command based on the characters provided

# Search by filtering entire search history
$ history | grep "xxx"        # searches for commands including xxx
{{</highlight>}}

## Useful commands

{{<highlight bash>}}

# Know when internet connection is up
$ ping 8.8.8.8 -a     # Makes periodic beeps when there is connectivity

# Show open ports
$ sudo lsof -ni

# Live read log files
tail -f /var/log/my-app/my-app.log | grep ERROR

# Simple image editing
# Must have imagemagick installed (apt-get install imagemagick)

# Append multiple images horizontally
convert +append input1.jpg input2.jpg output.jpg

# Append multiple images vertically
convert -append input1.jpg input2.jpg output.jpg

# Reize image
convert -resize 50% input.png output.png

# Add border to image
convert input.gif -shave 1x1 -bordercolor black -border 1 output.gif

{{</highlight>}}

<!-- Awesome Terminal Productivity
  https://github.com/chubin/cheat.sh
  https://github.com/tldr-pages/tldr
 -->
