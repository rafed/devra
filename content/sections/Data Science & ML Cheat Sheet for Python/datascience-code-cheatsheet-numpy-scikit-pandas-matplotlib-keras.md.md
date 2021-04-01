---
title: "My data science coding cheatsheet: Numpy, Scikit, Pandas, Matplotlib, Seaborn, Keras"
date: 2020-07-21
tags: [Machine learning, Data science, Programming]
description: The most effective code snippets in machine learning you'll ever need.
draft: true
---

I'm tired of looking up the same functions that I repeatedly use for my machine learning pipeline for loading, pre-processing, training and evaluating models. Now I'm on a mission to compile them all on this page.

### Table of Contents

- [Numpy](#numpy)
- [Pandas](#pandas)
- [Matplotlib](#matplotlib)
- [Scikit-learn](#scikit-learn)
  - [Dimnesionality reduction](#dimensionality-reduction)
  - [Pipelines](#pipelines)
- [Keras](#keras)

<!-- - [Training models](#training-models) -->

## Numpy
{{<highlight python>}}
import numpy as np
np.random.seed(42)  # Set random seed

a = np.arange(6)    # [0, 1, 2, 3, 4, 5]
a.reshape(3, 2)     # x-axis: 3, y-axis:2
a.T                 # Transpose matrix
{{</highlight>}}

## Pandas

### Read data
{{<highlight python>}}
import pandas as pd

df = pd.read_csv('file.csv', 
    header=None,        # Ignore first data row
    names=['h1', 'h2']  # Label columns
    index_col=0         # Set col 0 as index
)
{{</highlight>}}

### Filter data

{{<highlight python>}}
df = pd.concat([df1, df2], axis=1)     # Join DFs horizontally

df = df[df['h1']>18 & df['h2']==True]  # select rows with conditions
df = df[['h1', 'h2']]                  # Make subset with columns
df = df.drop(['h1', 'h2'], axis=1)     # Drop columns
{{</highlight>}}

### See data counts
{{<highlight python>}}
df['h1'].unique()       # => ['a', 'b', 'c']
df['h1'].nunique()      # => 3
df['h1'].value_counts() # => a:3, b:2, c:5

{{</highlight>}}

### Split data to train/test
{{<highlight python>}}
from sklearn.model_selection import train_test_split

x_train, x_test, y_train, y_test = train_test_split(
     df[['a', 'b']], df[['c']], test_size=0.20, random_state=42
)
{{</highlight>}}

### Remove correlated pairs

{{<highlight python>}}
def corr_pair(df):
    corr_matrix = df.corr().abs()    
    # Select upper triangle of correlation matrix
    upper = corr_matrix.where(np.triu(np.ones(corr_matrix.shape), k=1).astype(np.bool))
    to_drop = [column for column in upper.columns if any(upper[column] > 0.70)]
    return to_drop
{{</highlight>}}

## Matplotlib
{{<highlight python>}}
import matplotlib.pyplot as plt

# scatter plot
plt.scatter(x=list_x, y=list_y, alpha=0.5, c='green')
{{</highlight>}}

## Scikit-learn

### Dimensionality reduction

#### PCA

{{<highlight python>}}
from sklearn.decomposition import PCA
pca = PCA(n_components=2)
pca_result = pca.fit_transform(df)
x = pca_result[:,0]
y = pca_result[:,1]
{{</highlight>}}

#### TSNE

{{<highlight python>}}
from sklearn.manifold import TSNE
tsne = TSNE(n_components=2, perplexity=40, n_iter=300, random_state=42)
tsne_results = tsne.fit_transform(data_subset)
x = tsne_results[:,0]
y = tsne_results[:,1]
{{</highlight>}}

<!-- ### Training models

{{<highlight python>}}
import sklearn
{{</highlight>}} -->

### Pipelines

#### Kfold

{{<highlight python>}}
from sklearn.model_selection KFold, StratifiedKFold, cross_validate

kfold = KFold(n_splits=10, shuffle=True, random_state=RS)
# or
kfold = StratifiedKFold(n_splits=10, shuffle=True, random_state=RS)

models = []
models.append(("KNeighbors",KNeighborsClassifier()))
models.append(("DecisionTree",DecisionTreeClassifier()))

scorers = ['precision','recall', 'f1_macro','roc_auc','balanced_accuracy']

for name, model in models:
    result = cross_validate(model, x, y, cv=kfold, scoring=scorers)
    for sc in scorers:
        sc = f"test_{sc}"
        print(f"{name} {sc} {result[sc].mean():.3f}")
{{</highlight>}}

## Keras

### Sequential

{{<highlight python>}}
import tensorflow as tf
from tensorflow.keras.models import Sequential

seq_model = Sequential([
  tf.keras.layers.Dense(2400, input_dim=2400, activation='relu'),
  tf.keras.layers.Dense(1000, activation='relu'),
  tf.keras.layers.Dense(2)
])

seq_model.compile(optimizer='adam',
              loss='binary_crossentropy',
              metrics=['accuracy'])

seq_model.fit(train_x, train_y, epochs=150, batch_size=5)
_, accuracy = seq_model.evaluate(test_x, test_y)
print('Accuracy: %.2f' % (accuracy*100))
{{</highlight>}}

### CNN
{{<highlight python>}}
import tensorflow as tf
from tensorflow.keras.models import Sequential

model = Sequential([
    tf.keras.layers.Conv2D(4, (3,3), padding='same', activation='relu',
                           input_shape=(1, 2, 1200)),
    tf.keras.layers.MaxPooling2D((1, 1),),

    tf.keras.layers.Conv2D(8, (3,3), padding='same', activation='relu'),
    tf.keras.layers.MaxPooling2D((1, 1)),

    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(32, activation='relu'),
    tf.keras.layers.Dense(2, activation='softmax')
])

model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy']) 
model.summary()
{{</highlight>}}
