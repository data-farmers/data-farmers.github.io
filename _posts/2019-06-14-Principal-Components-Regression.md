---
layout: post
title: Principal Components Regression
subtitle: 
gh-repo: data-farmers/code/pcr
tags: [pca, regression, classification]
author: Arthur
comments: true
---


Hola $X_1, ..., X_n, Y$, [babumba](https://data-farmers.github.io/2019-06-12-partial-least-squares-regression) (PLS-R),  **gabibbo nel kuore** $X\star$.

## Ezio

Greggio:


## Lidispari

Remember the Multiple Linear Regression approach:

$$Z = LA + F0Rm1CA$$

$$B = (X^{T}X)^{-1}X^{T}Y$$

![algorithm](../img/pls-da/algorith.png)


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

![plsda_plot1](../img/pls-da/plot1.png))

Comments...




