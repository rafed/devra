---
title: Fix bulma mobile view problem
date: 2020-05-16
tags: [WebDev]
description: Fix a mobile view problem in bulma CSS.
---

I've been working with bulma for a while. Although the desktop rendering worked well, there were issues with the mobile view:

#### Problem

1. There is like a white border on the right
2. The screen is scrollable towards the right (which should not be)

{{<local-img src="image/bulmafix/problem.gif" caption="Problem">}}

#### Problem fix

To fix this, add the following code

{{<highlight css>}}
.columns {
    margin: 0;
}
{{</highlight>}}

With the above css it should render properly.

{{<local-img src="image/bulmafix/fixed.gif" caption="Problem fixed">}}
