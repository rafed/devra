---
title: Why I Switched Back to Github Pages from Blogger.com
date: 2020-05-20
tags: [blogging, web]
image: "hugo-icon.png"
---

Previously I used to blog on Github pages with Jekyll. After I discovered blogger.com, I thought I could improve my blogging experience with it. So I made the switch and these were my reasons.

1. I couldn't find a suitable Jekyll theme for my blog. So I made one for myself. Not being a good UI designer, I made a pretty bad theme.  With Blogger.com's WYSIWYG editor I thought I could make a better looking site.
1. I liked managing blog posts in the browser rather than with a text editor locally.
1. The fact that my blog was in the cloud and I could access it from any PC was appealing. With Github pages I was limited to my local machine. Working from other PCs is possible but it required the hassle of git clones and git configs.
1. Blogger.com comes with a neat mobile app that makes writing on the go possible (even offline).
1. Blogger.com has inbuilt support for comments and user analytics. In Github pages plugins (such as disqus and google analytics) were required.

Blogger seemed like the appropriate platform for me. But after publishing about 20 posts problems started popping out.

1. The text editor in blogger is terrible. When you edit multiple posts at a time, there shows some erratic behaviors. I lost freshly written articles twice after trying to perform undo operations. (Although as of today, while writing this post, I did notice the platform is upgrading it's UI. Hopefully this will be fixed)
1. The WYSIWYG theme editor is good, but I did not seem to have complete control over it. I couldn't change a theme's layout the way I wanted to which I could do with HTML and CSS.
1. After losing two articles, I realized they did not have a good backup keeping option. Keeping backups and restoring backups was painful and not user friendly.
1. And the most important thing why I came back to Github was **Hugo**

Hugo is a static site generator like Jekyll and it seemed to be quite hyped. So I tried out the hype train and it was quite the ride. 

Hugo is much more simpler and faster than and I immediately fell in love with it. What felt very hard to do with Jekyll, I could do it easily with Hugo (Or maybe I just became a better developer over time and more confident with my skills.)

So I finally made a theme called [Ramium](https://github.com/rafed/ramium) which perfectly suits my needs. It's open-sourced and you can find it at [github.com/rafed/ramium](https://github.com/rafed/ramium). This very blog is made with Hugo and Ramium. If you like it give it a star!
