---
title: Bare Minimum Multi-Tasking Guide for the Terminal with Tmux
date: 2019-09-29
lastmod: 20202-05-15
tags: [terminal, linux]
image: "tmux.png"
---

Have you ever-
- SSHed to a server and felt the need of another terminal session because the current one was already running something? 
- SSHed to a server to run a long-running process but couldn't close the terminal because it would terminate the process?
- Wanted to wok with multi-window terminal like the picture above?
- Wanted to continue from where you left off your terminal the last time?

If your answers to the questions are yes, then Tmux is the tool you need. Tmux is a multiplexer for the Linux terminal. In simple words, you can split a terminal and make multiple tabs in it with Tmux. There are many complete guides for Tmux. However, here I'm noting down the most important commands and the ones I use the most.

## Installation

If Tmux is not installed, install it by running-
{{<highlight bash>}}
$ sudo apt  install tmux 
# or install with snap
$ sudo snap install tmux 
{{</highlight>}}

## Commands

Create a new tmux session at first.

{{<highlight bash>}}
$ tmux #Create a new tmux session
{{</highlight>}}

You can do the following in a tmux session.

<pre>
<kbd>Ctrl+b</kbd> <kbd>c</kbd>  Create a new window
<kbd>Ctrl+b</kbd> <kbd>n</kbd>  Go to next window
<kbd>Ctrl+b</kbd> <kbd>0</kbd>  Switch to window 0 (do for any number of windows: 1, 2, 3...)
<kbd>Ctrl+b</kbd> <kbd>w</kbd>  Graphically switch window (choose from a list, also shows the snap of a session)
<kbd>Ctrl+b</kbd> <kbd>x</kbd>  Kill current window
<kbd>Ctrl+b</kbd> <kbd>d</kbd>  Detach session (doesn't terminate the session, simply gets out of tmux)
</pre>

After detaching from a session you can attach to that session.

{{<highlight bash>}}
$ tmux ls               # See available tmux sessions
$ tmux a                # Attach to last used session
$ tmux a -t <session>   # Attach to a specific session from all available sessions (do "tmux ls" to view the sessions first)
{{</highlight>}}

## Not necessary but useful commands

The above commands are all you need to take advantage of the most of tmux. However, if you want some terminal splitting, then-

<pre>
<kbd>Ctrl+b</kbd> <kbd>%</kbd>                    Split terminal horizontally
<kbd>Ctrl+b</kbd> <kbd>"</kbd>                    Split terminal vertically
<kbd>Ctrl+b</kbd> <kbd>[arrow keys]</kbd>         Switch to another split screen
[hold] <kbd>Ctrl+b</kbd> <kbd>[arrow keys]</kbd>  Change size of the current split screen
<kbd>Ctrl+b</kbd> <kbd>t</kbd>                    Shows time!
</pre>
