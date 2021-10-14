---
title: Racial Bias in AI (and how I got Embarrassed)
date: 2021-10-13
tags: [machine learning, misc]
image: thumbnail.png
---

Humans often wrongly discriminate based on skin color, religion and beliefs. Whether this increases or decreases every day we cannot tell for certain. But what we can tell, as data-driven apps continue to grow, computer-based discrimination will increase. Yes, computers can be racist too. And this is the story of how I embarrassingly happened to be in the part of making one.

## The Back Story

I was a student in 2018. Me and two of my friends built an augmented reality project called [virtual trial room](https://rafed.github.io/project/virtual-trial-room/). The idea was simple. You pick a dress that you like and stand in front of a webcam. The app would then detect the person using object detection and overlay the dress over them in real-time. This would give an impression of how a dress would look/fit on you. The concept worked similarly for sunglasses and hats.

We participated in a few competitions with this project and it was quite a success. However, the one place we did not succeed was in a competition held at **Islamic University of Technology (IUT)**.

IUT is one of the leading universities in Bangladesh that hosts more foreign students than any other in the country through scholarship programs. A lot of their foreign students come from African countries.

We reached IUT early in the morning. We set up our stall and started demonstrating our project to interested guests. Many people tried using it and found it to be fun and engaging. Everything was going well until our African guests started to come in.

Whenever an African guest tried to use the app, it wouldn't detect them. This was an unexpected behavior. During testing, our app had never failed to detect a person before. We had tested the app with at least 100s of friends and family members of different ages and in different lighting conditions. But for some reason, this time it did not work. Our app relied heavily on facial recognition. And for the first time, our app could not detect any face.

My teammates thought something was wrong with the app and tried restarting it as well as repositioning the guests and changing camera angles. But I stood there in horror. I knew exactly what had happened. And I knew we couldn't fix this now. The face detection model we used did not have training samples of darker-skinned people. So it essentially worked on people who were white or brown-skinned.

Of course, we made excuses while the app wouldn't work. _"There are too many people in the background disturbing our algorithm"_ or _"the lighting is inadequate"_. We did manage to convince many of our customers, but some of them saw right through it. One of our guests asked me, "Why does it not work for me? Is it because I'm black?"

This was too much of an embarrassment for us. I apologized straight away and explained to him in detail what had happened.

## Racial Bias in AI: Causes, Examples, and Solutions

If an algorithm/model discriminates between people based on their ethnicity or beliefs then it is said to have a racial bias. It is usually unconscious and intended (but can be sometimes be conscious as well).

Other examples of racial bias that have been observed:
* Self-driving cars are more likely to recognize white pedestrians than Black pedestrians.
* Criminal risk assessment technology has led to Black individuals being sentenced to harsher criminal sentences.
* Healthcare company has used an algorithm that deemed Black patients less worthy of critical healthcare.
* Fin-tech companies have been shown to discriminate against Black households via higher mortgage interest rates.

The most common reason for racial bias is the use of low-quality datasets. A dataset is of low quality when sampling is done incorrectly. When it comes to data-driven apps, "garbage in, garbage out." 

If a dataset cannot be improved by collecting new data points, it can be mitigated through oversampling or undersampling. Oversampling randomly duplicates data points in the minority dataset to the quantity of the majority. And, undersampling randomly reduces the number of data points in the majority to the minority.


## Conclusion

Yes, we lost that competition. But we learned a valuable lesson on racial bias. Let our lesson be an example for others so that they don't have to face the same sort of embarrassment, or worse, make an app that makes critical decisions with racial bias. We want racism to stop from humans and computers.

##### References
* [www.credera.com/insights/racial-bias-in-machine-learning-and-artificial-intelligence](https://www.credera.com/insights/racial-bias-in-machine-learning-and-artificial-intelligence)