---
layout: post
title: Bootstrap and Random Forest
key: 20201103
tags:
  - Python
  - machine learning
  - random forest
  - decision tree
  - bootstrap
  - sklearn
  - overfitting
---

# Bootstrap

## What is Bootstrap Sampling?

In statistics, Bootstrap Sampling is a method that involves drawing of sample data repreatedly with replacement from a data source to estimate a population parameter.

* Sampling: with respect to statistics, sampling is the process of selectign a subset of items from a vast collection of items to estimate a certain characteristic of the entire population.

<!--more-->

## Why do we need Bootstrap Sampling?

Let’s say we want to find the mean height of all the students in a school (which has a total population of 1,000). So, how can we perform this task?

One approach is to measure the height of all the students and then compute the mean height. I’ve illustrated this process below:

![bootstrap_demp](https://raw.githubusercontent.com/hadleyhzy34/machine_learning/master/random_forest/source/bootstrap_demo.png)

However, this would be a tedious task. Just think about it, we would have to individually measure the heights of 1,000 students and then compute the mean height. It will take days! We need a smarter approach here.

This is where Bootstrap Sampling comes into play.

Instead of measuring the heights of all the students, we can draw a random sample of 5 students and measure their heights. We would repeat this process 20 times and then average the collected height data of 100 students (5 x 20). This average height would be an estimate of the mean height of all the students of the school.


## Bootstrap Sampling in Machine Learning

Bootstrap sampling is used in a machine learning ensemble algorithm called bootstrap aggregating (also called bagging). It helps in avoiding overfitting and improves the stability of machine learning algorithms.

In bagging, a certain number of equally sized subsets of a dataset are extracted with replacement. Then, a machine learning algorithm is applied to each of these subsets and the outputs are ensembled as I have illustrated below:

![ensemble_bagging](https://raw.githubusercontent.com/hadleyhzy34/machine_learning/master/random_forest/source/Ensemble_Bagging.svg)

* Ensemble

* Bagging

## Implement Bootstrap Sampling in Python

```python
import numpy as np
import seaborn as sns
import random
```

normal distribution dataset


```python
x = np.random.normal(loc=500.0,scale=1.0,size=10000)
np.mean(x)
```




    500.0033021822781




```python
sample_mean = []

#bootstrap sampling
for i in range(10000):
    y = random.sample(x.tolist(), 5)
    avg = np.mean(y)
    sample_mean.append(avg)
    # print(avg)
```


```python
np.mean(sample_mean)
```




    500.00585544721156


Task:
1. size of sample data compared to whole training data

* In Random Forest, the bootstrap sample size of even 20% gives a pretty good performance

2. overfit




