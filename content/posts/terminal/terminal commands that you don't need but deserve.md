---
title: 13 terminal commands that you don't need but deserve
date: 2020-07-07
tags: [terminal, linux]
---

The Linux terminal is not all boring and dull. Spice up your life with these fun and awesome commands. <!--more-->

The programs mentioned require very little disk space. So don't miss them out by not installing.

## 1. xeyes

A pair of eyes that stares at your cursor for no reason at all.

{{<highlight bash>}}
# apt-get install x11-apps
$ xeyes
{{</highlight>}}

## 2. spd-say

Turn text to weird robotic speech!

{{<highlight bash>}}
# sudo apt-get install speech-dispatcher
$ spd-say "hello world"
{{</highlight>}}

Here's a bit of fun advice. Put **spd-say "your computer has been hacked"** on your friend's **~/.bashrc file** and watch them freak out every time they turn on the terminal.

## 3. parrot.live

Watch a parrot move with the groove.

{{<highlight bash>}}
$ curl parrot.live
{{</highlight>}}

## 4. towel.blinkenlights.nl

Watch the classic star wars movie in the terminal.

{{<highlight bash>}}
$ telnet towel.blinkenlights.nl
{{</highlight>}}

## 5. oneko 

Watch your mouse being chased by a fluffy cat.

{{<highlight bash>}}
# sudo apt-get install oneko
$ oneko

# for dog
$ oneko -dog
{{</highlight>}}

Check out more options in the man page.

## 6. apt-get moo

Easter egg for apt-get. Doesn't install anything.

{{<highlight bash>}}
$ apt-get moo
{{</highlight>}}

## 7. sl (steam locomotive)

Watch a train go by every time you enter _sl_ instead of _ls_.

{{<highlight bash>}}
# apt-get install sl
$ sl
{{</highlight>}}

## 8. cowsay/cowthink

{{<highlight bash>}}
# apt-get install cowsay
$ cowsay "welcome to devra"
 __________________
< welcome to devra >
 ------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

# also try with cowthink
$ cowthink "hello world"
{{</highlight>}}

## 9. fortune

Print a random, hopefully interesting statement.

{{<highlight bash>}}
# apt-get install fortune
$ fortune

Q:	How many bureaucrats does it take to screw in a light bulb?
A:	Two.  One to assure everyone that everything possible is being
	done while the other screws the bulb into the water faucet.

# for short statements only add -s flag
$ fortune -s

Avoid gunfire in the bathroom tonight.
{{</highlight>}}

Check out the man pages for more options.

## 10. toilet

Print banners in the terminal.

{{<highlight bash>}}
# apt-get install toilet
$ toilet "DevRa" 

      #                             
   mmm#   mmm   m   m   m mm   mmm  
  #" "#  #"  #  "m m"   #"  " "   # 
  #   #  #""""   #m#    #     m"""# 
  "#m##  "#mm"    #     #     "mm"#
{{</highlight>}}

## 11. cmatrix

Show off like a hacker with this matrix themed screen saver for the terminal.

{{<highlight bash>}}
# apt-get install cmatrix
$ cmatrix -s 
{{</highlight>}}

Check out the man pages for options.

## 12. aview

Turn images into ascii art.

{{<highlight bash>}}
# sudo apt-get install aview
$ asciiview input.png -driver curses
{{</highlight>}}

## 13. aafire/cacafire

Burn your terminal to the ground! (No, it's not gonna overheat)

{{<highlight bash>}}
# apt-get install libaa-bin
$ aafire -driver curses
{{</highlight>}}

Or try the colored version

{{<highlight bash>}}
# apt-get install caca-utils
$ cacafire
{{</highlight>}}
