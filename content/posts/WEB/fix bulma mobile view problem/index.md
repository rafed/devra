---
title: Fix Bulma Mobile View Problem
date: 2020-05-16
tags: [web, frontend]
description: Fix a mobile view problem in bulma CSS.
image: bulma.png
---

I've been working with bulma for a while. Although the desktop rendering worked well, there were issues with the mobile view:

#### Problem

1. There is like a white border on the right
2. The screen is scrollable towards the right (which should not be)

![Bulmda problem](./problem.gif)

#### Problem fix

To fix this, add the following code

{{<highlight css>}}
.columns {
    margin: 0;
}
{{</highlight>}}

With the above css it should render properly.

![Bulma problem fixed](./fixed.gif)
