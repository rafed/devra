---
title: "My data science coding cheatsheet: Numpy, Scikit, Pandas, Matplotlib, Keras"
date: 2020-06-09
tags: [Machine learning, Data science, Programming]
description: A rudimentary image processing technique with K-means
draft: true
---

I'm tired of looking up the same functions that I repeatedly use for my machine learning pipeline for loading, pre-processing, training and evaluating models. Now I'm on a mission to compile them all on this page.

### Shortcuts

- [Numpy](#numpy)
- [Pandas](#pandas)
- [Matplotlib](#matplotlib)
- [Scikit-learn](#scikit-learn)
- [Keras](#keras)

## Numpy
{{<highlight python>}}
import numpy as np
np.random.seed(42)  # Set random seed
{{</highlight>}}

## Pandas
{{<highlight python>}}
import pandas as pd

df = pd.read_csv('file.csv', 
    header=None,        # Ignore first data row
    names=['h1', 'h2']  # Label columns
    index_col=0         # Set col 0 as index
)

df = pd.concat([df1, df2], axis=1) # Join DFs horizontally

df = df[df['h1']>18 & df['h2']==True]  # select rows with conditions
df = df[['h1', 'h2']]                  # Make subset with columns
df = df.drop(['h1', 'h2'], axis=1)     # Drop columns

df['h1'].unique()       # => ['a', 'b', 'c']
df['h1'].nunique()      # => 3
df['h1'].value_counts() # => a:3, b:2, c:5

{{</highlight>}}

## Matplotlib
{{<highlight python>}}
import matplotlib.pyplot as plt
{{</highlight>}}

## Scikit-learn
{{<highlight python>}}
import sklearn
{{</highlight>}}

## Keras
{{<highlight python>}}
import tensorflow as tf
{{</highlight>}}
