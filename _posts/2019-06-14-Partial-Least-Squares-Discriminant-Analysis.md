---
layout: post
title: Partial Least Squares Discriminant Analysis
subtitle: A PLS-R variant for categorical variables
gh-repo: data-farmers/code/pls-da
tags: [multidimensional-scaling, regression, classification]
author: Alfonso
comments: true
---


It may happen that you have a dataset with columns X_1, ..., X_n, Y, and you want to check if there is any correlation between X_1, ..., X_n variables (or part of them) and the Y variable. You know that correlation doesn't mean causation, but sometimes it would be useful to assess wether one could say anything on Y by looking at Xs variables, i.e. finding some vector B that $Y \simeq XB$. A well known algorithm for such a task is the [Partial Least Squares Regression](https://data-farmers.github.io/2019-06-12-partial-least-squares-regression) (PLS-R), but it need Y variable to be continous, such as Xs; in case you have categorical variables, you can use a variant: Partial Least Squares Discriminant Analysis (PLS-DA). In a hypothetical taxonomy of ML methods, one could be doubtful about where to place PLS-DA, as it solves two problems with a single algorithm: (1) it encompassess a **feature dimensionality reduction** step, and (2) it provides a B vector that can be reused for **predicting** $Y\star$ from future observations $X\star$.

## Purpose

Let's start from the dimensionality reduction task. You know your Xs variables (from now on: **predictors**) could be related somewhat to your Y (**response vector**), but X is high in dimensionality and you'd better use a subset - or a lower dimensional linear projection - of it. Let's call them **LV** (Latent Variables). Did you hear PCA? Yes, good point, I could say also LDA, but there are some differences between these algorithms that is going to affect your work significantly:


**PLS-DA vs LDA**: Some kind of data, spectral data for instance, tend to have more features than observations. In such a high-dimensional space, features are often correlated each other, a problem known as multicollinearity. Unlike PLS-DA, LDA cannot handle multicollinearity.


**PLS-DA vs PCA**: PCA is completely unsupervised, i.e. you don't know in advance if there are classes in your dataset, hence you simply project it into a space which maximizes the variance between your data, hopeful it will lead to a good qualitative clusterization. In PLS-DA, however, you know how your dataset is divided in classes from the response vector Y. The goal here is then to project the predictors into a space, while maximizing the between-group distances. PCA and PLS-DA projections will eventually be different.

Due to these differences, PLS-DA is the best choice when dealing with dataset with less observation than features, and you know which class each observation belongs to.
Hence we learned a transformation from the original n-dimensional spaced into the new P-dimensional space, where P is the number of Latent Variables, in a way that separates the most our data into the different classes. This mapping can turn useful in the future: if we gather new unlabelled data, we can map them through this projection, and accordingly classify them.


## The algorithm

1) equations Y = BX + E
2) Algorithm


## The code

1) transformation Y -> [0|1]
2) do we need any pre-processing?
3) code!

```python
return whatever
```

201

{: .box-note}
**Note:** Fuck.


