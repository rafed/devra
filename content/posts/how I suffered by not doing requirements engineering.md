---
title: How I suffered by not doing Requirements Engineering
date: 2020-06-20
tags: [Requirements engineering, Software engineering]
---

Recently one of my relatives asked me if I could build an eCommerce site for their family clothing business. Since I was busy and couldn't manage the time to do it myself I forwarded the task to two of my fellow juniors. I would just be a middleman connecting both sides and supervise the project.

A plain eCommerce site is trivial these days. The business logic of eCommerce sites have been quite standardized. The tooling to build them is also abundant. You can simply select a WordPress theme and deploy a site in a few days. 

The clients requested the site to be finished within two weeks because Eid was approaching and they wanted to catch the online market. Eid festival is a major occasion when cloth selling booms. Catching the online market was also important for their business as covid19 was pushing people to buy everything online.

Since the task was trivial and time was short, I did not bother going into the details of what will be implemented and review it by the clients.

Turns out this was a bad mistake.

The guys working on the project are great developers. They managed to put up a site using a theme. However, the client did not like the UI and asked for modifications that were beyond the scope of the theme.

This is where the problems started.

Even though it would be difficult, my developers attempted to meet those demands by modifying internal HTML and CSS. For example converting dropdowns to mega menus, changing margins and adding/removing components. Turns out it was a pretty bad idea. The theme lost its beauty and the site looked like crap. Modifying a manually coded site is no big deal. But on a WordPress theme that does not support it, it's very hard to change. Time was also running out.

This was when I realized we should have talked about how the site would look like by consulting the themes with the clients.

We eventually conducted a meeting and agreed on a theme that the clients liked. The site was rebuilt from scratch and everyone was ok. But what was frustrating for the developers was that they had to do twice the work for the payment of one.

We could not claim the payment of the extra work done because we did not have that leverage. We did not fix and finalize what we will deliver. Rather we agreed we'd deliver what the client wanted. Had we finalized and sealed the requirements, for every major change on the site we could put a price on the effort needed to implement that change.

So, my lessons learned are:
1. Always collect requirements and form a checklist, no matter how trivial they may seem.
2. Before implementing, seal a contract on what you're going to implement. So that, for any extra work outside the contract you can charge your deserved pay.
