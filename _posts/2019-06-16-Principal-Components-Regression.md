---
layout: post
title: Principal Components Regression
subtitle: 
gh-repo: data-farmers/code/pcr
tags: [pca, regression, classification]
author: Arthur
comments: true
---

Principal Components Regression (PCR) is a regression technique based on principal component analysis (PCA).

The basic idea behind PCR is to calculate the principal components and then, instead of using the original observed covariates, use some of these components as predictors in a linear regression model fitted using the typical least squares procedure.

The PCR method can be divided into three steps:

1) Perform PCA method on the observed data matrix for the explanatory variables to obtain the principal components, and then select a subset.

2) Regress the observed vector of outcomes on the selected principal components as covariates, using ordinary least squares regression (linear regression) to get a vector of estimated regression coefficients (with dimension equal to the number of selected principal components).

3) Transform the obtained vector at step 2 back to the scale of the actual covariates.

## The method

The idea behind Principal Components Regression is very seample, instead of going haed with the original set of observed covariates, we will reduce this set using Principal Components Analysis (PCA).
Basically, PCA is a dimension reduction technique that combines features.

It converts a set of observations of possibly correlated variables into a set of values of linearly uncorrelated variables called **principal components**. If there are $n$ observations with $p$ variables, then the number of distinct principal components is $min(n-1, p)$.
This transformation is defined in such a way that the first principal component has the largest possible variance, and each succeeding component in turn has the highest variance possible under the constraint that it is orthogonal to the preceding components.

Imagine we have a linear regression with two indipendent variable ($x_1$ and $x_2$):

$y = b_01 + b_1x_1 + b_2x_2$

The variation in $y$ explained by $x_1$ and $x_2$, will also be explained with a similar extent by a combined variable:

$z_1 = a_1x_1 + a_2x_2$

So, $z_1$ will replace $b_1x_1 + b_2x_2$. For reducing the dimension, the number of principal component that is going to be used, will always be less than the number of features.

It's important to remember that PCA is not a feature selection method: we're not selecting features, we're rather combining features to come up with a new feature.

Now, from a set of features, for example $(x_1, x_2, x_3, x_4, x_5)^T$ we come up to a set of principle component $(z_1, z_2)^T$.
In ordinary least squares we would have used all the predictors.

OLS:	$y = b_01 + b_1x_1 + b_2x_2 + b_3x_3 + b_4x_4 + b_5x_5$

In PCR we are going to use a smaller set, the principle component:

PCR:	$y = b^i_01 + b^i_1z_1 + b^i_2z_2$

## Pros and cons of PCR

Some of the most notable advantages of performing PCR are the following:

-	**Dimensionality reduction**. By using PCR you can easily perform dimensionality reduction on a high dimensional dataset and then fit a linear regression model to a smaller set of variables, while at the same time keep most of the variability of the original predictors.
You can also run PCR when there are more variables than observations (wide data).
PCR tends to perform well when the first principal components are enough to explain most of the variation in the predictors.

-	**Overfitting reduction**. Overfitting is the result of using a too complex model. Most of the information related to the dependent variable is condensend in the principal components and by estimating less coefficients you can reduce the risk of overfitting.

-	PCR can perform regression when the explanatory variables are **highly correlated** or even collinear.

-	PCR is **automatic**: The only decision you need to make is how many principal components to keep.



As always with potential benefits come potential risks and drawbacks.

-	Principal component regression does not consider the **response variable** when deciding which principal components to drop: it could very well be that some of
the “last” principal components are useful for predicting $Y$!
The decision to drop components is based only on the magnitude of the variance of the components. There is no a priori reason to believe that the principal components with the largest variance are the components that best predict the response. 

-	**Dimensionality reduction**. In case you need a lot of principal components to explain most of the variability in your data, say roughly as many principal components as the number of variables in your dataset, then PCR might not perform that well in that scenario, it might even be worse than plain vanilla linear regression.

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