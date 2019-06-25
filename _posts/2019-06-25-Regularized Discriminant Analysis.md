---
layout: post
title: Regularized Discriminant Analysis
subtitle: 
gh-repo: data-farmers/code/pcr
tags: [pca, regression, classification]
author: Potente Opossum
comments: true
---

Often (?!) we have to deal with questions like ‘are the groups different?’, ‘on what variables, are the groups most different?’, ‘can one predict which group a person belongs to using such variables?’ In answering such questions, discriminant analysis is quite helpful.

Today I'll present you the following approaches to discriminant analysis:
-	Quadratic Discriminant Analysis,
-	Linear Discriminant Analysis,
-	Regularized Discriminant Analysis,




## Discriminant Analysis

The purpose of discriminant analysis is to assign objects to one
of several (K) groups based on a set of measurements obtained from each object $X = (X_1, X_2, ..., X_p)$.
Each object is assumed to be a member of one (and only one) group $1 ≤ k ≤ K$ and, obviously, an error is incurred if the object is attached to the wrong group. The measurements of all objects of one class k are
characterized by a probability density $f_k(X)$ and we want to find a rule to decide for every object to wich group k it belongs to.

**Example**

Let's make an exmple to better understand what we're taliking about.
We've a group of people, male and famale. We just know weight and height of each person in the group and we want to classify the gender for each person from the weight and height (discriminant analysis).
So we have $K = 2$ (two groups) and $p = 2$ (two kind of measurements). 
We have a classification rule (discriminant function) to choose the group for each person and to costruct this function we use a training sample in which the gender is already known.

**Class distribution**

We have a conditional distribution for each class k, infact the distribution of the measurements X are seldom identical in each class.
Most often applied classifcation rules are based on the multivariate normal distribution:

![alt text](../img/RDA/multivariate_normal_dist.png "multivariate normal distribution")

where $\mu$ and $\sum_k$ are the class k $(1 \le k \le K)$ population mean vector ($\mu$) and covariance matrix ($\sum_k$).

**Prior and unconditional distribution**

Prior probability: we can have some prior knowledge about the probability of observing a member of class $k$: $\pi_k with \pi_1 + ... + \pi_k = 1$. If the prior probabilities are eqia; for each k, this leads to Maximum-Likelihood.

To estimate the class conditional densities $f_k(X)$ and the prior
probability $\pi_k$, a training sample with already correctly classified classes is used:

Unconditional distribution of $X$ =$ f(X) = \sum_{k=1}^{K}\pi(k)f(X|k)$

**Posterior distribution**

The probability for one object with given vector $X^T = (X_1, ..., X_p)$ to belong to a class $k$ is calculated by the Bayes forumla:

$p(k|X)$



## The Code

```python
from sklearn.cross_decomposition import PLSRegression

#Read the dataset
df = pd.read_csv('seeds.csv')
X = df.iloc[:,0:7]
y = df['Type']

#Create train set and test set
train, test, train_lbl, test_lbl = train_test_split(X, y, test_size=1/7.0, random_state=0)

#Scale the data: mean 0 and variance 1 
scaler = StandardScaler()
# Fit on training set only.
scaler.fit(train)
train = scaler.transform(train)
test = scaler.transform(test)

pca = PCA(n_components=nc)
pca.fit(train)
train = pca.transform(train)
test = pca.transform(test)

```


<!--
## The code


| Label | Y |
| :------ |:--- |
| A | 1 |
| B | 0 |


`sklearn`

```python
from sklearn.cross_decomposition import PLSRegression

# 2 Latent Variables, no scaling
plsr = PLSRegression(n_components=2, scale=False)

# PLS-DA algorithm
plsr.fit(X, Y)

# Just print the resulting scores
plsr.x_scores_
```

`plsr.x_scores_` 

-->