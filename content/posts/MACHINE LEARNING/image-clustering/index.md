---
title: Image Clustering
date: 2017-09-18
tags: [programming, machine learning]
image: cluster.png
description: A rudimentary image processing technique with K-means
---

Clustering is a technique to group similar elements together. The following shows a simple program codebase is a small attempt to cluster colors in images.

At the heart of the program lies the **K-Means algorithm**. The source is available at [github.com/rafed/Image-clustering](https://github.com/rafed123/Image-clustering).

|Original|  Averaged - 2 clusters	| Averaged - 6 clusters|
|:-------------:|:---------------:|:----------:|
|![Original image](https://github.com/rafed/Image-clustering/blob/master/img/original?raw=true) | ![Averaged - 2 clusters](https://github.com/rafed/Image-clustering/blob/master/img/avg2?raw=true) | ![Averaged - 6 clusters](https://github.com/rafed/Image-clustering/blob/master/img/avg6?raw=true)

Look at the "original image" above. There are pixels of many different colors. How many different colors exist is not of our interest. What we're interested in is that we'll create color groups in the image that are similar. We will specify how many clusters we want and the program will output an image with that many clusters. In the second image, the first image is represented using only 2 colors! The third image with only 6 colors! 

|Original|  Averaged - 2 clusters	| Averaged - 6 clusters|
|:-------------:|:---------------:|:----------:|
|![Original image](https://github.com/rafed/Image-clustering/blob/master/img/lenna?raw=true) | ![Averaged - 2 clusters](https://github.com/rafed/Image-clustering/blob/master/img/len2?raw=true) | ![Averaged - 6 clusters](https://github.com/rafed/Image-clustering/blob/master/img/len10?raw=true)

## Features of the program

* Cluster (by averaging) - averages the color in a particular group (1st example)
* Cluster (by color) - select a random color for a particular group (2nd example)
* increase/decrease brightness and contrast

## Running the project

Download the source code [here](https://github.com/rafed/Image-clustering). It is a Java project you can directly import to eclipse IDE.

In Main.java, tweak the following:  

{{<highlight java>}}
int numOfClusters = 10;         // num of clusters to make
int numOfKmeansIteration = 5;   
int type = averaged;            // (averaged/colored)
int comparisonOn = hue;         // (comparison color based on hue/brightness/saturation)
int contrast = 0;               // +/- contrast
int brightness = 0;             // +/- brightness
{{</highlight>}}

First try out **numOfClusters** and **type** to have some fun. Then play with brightness and contrast to fine-tune the image. Specify your path to the input file and output path and you're ready to go!

## K-Means

K-means is an **unsupervised machine learning** algorithm.  Which basically means it can describe a hidden structure from unlabeled data. In our case, it finds clusters, without us providing information on where to look for it. It is one of the easiest machine learning algorithms to implement. If you're interested in machine learning consider learning this. It's one of the easiest algorithm out there.
