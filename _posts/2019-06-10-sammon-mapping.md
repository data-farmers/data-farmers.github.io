---
layout: post
title: Sammon mapping
subtitle: A non-linear mapping for data visualization
gh-repo: data-farmers/code
tags: [multidimensional-scaling, non-linear]
author: Alfonso
comments: true
---


Sammon Mapping belongs to the multidimensional scaling algorithms family, as its main goal is to reduce a high dimensionality
space to a lower dimensionality space, for visualization purposes. Unlike PCA and other dimensionality scaling algorithms, 
Sammon Mapping's aim is not to highlight the most descriptive component to project the original data points onto, but rather 
to represent more or less the same "structure" of the original data, even when flattened in lower dimensionality space, 
highlighting patterns and spatial relationships.

## Purpose

Drawing points in the space is pretty easy if the space is 1, 2 or 3 dimensional. In order to represent higher dimensional spaces, 
one could apply some dimensionality reduction algorithm, keeping the best 2 or 3 axes of the space, or some combination.
This kind of projection usually distorts distances between points, mapping them in a space where they don't have the same shape.
Sammon Mapping, instead, points to flatten a high dimensionality space preserving, when possible, the distance between any pair of points.
Take a look at these pictures I took from [this amazing explanation](http://homepages.inf.ed.ac.uk/rbf/CVonline/LOCAL_COPIES/AV0910/henderson.pdf): 

![Sammon1](img/sammon/sammon1.png)
![Sammon2](img/sammon/sammon2.png)

Sammon Mapping is then a perfect start for visualizing your high dimensionality dataset, searching for recurrent structures and shapes.

## The algorithm

As proposed by J. W. Sammon in 1969, Sammon Mapping is not actually an algorithm, strictly speaking. Sammon defined an error funcion,
in order to evaluate how good a given projection is in preserving the original structure, by assessing the difference in the distance between each pair of points
_i_ and _j_ in the higher and in the lower dimensionality space. Following his original proposal, the function error E is a function of the
Euclidean distance, as follows:

**FORMULA**

where _variables_ means _whatever.

Thus, the projection itself is a optimization problem: for each pair of points {_i_, _j_}, we only need to find a new distance which is as close as possible to the original one,
where "as close as possible" means beneath a given threshold \begin{equation} \epsilon \end{equation}.
Sammon proposed a steepest gradient descent algorithm to minimize the error, a method easy to apply but poor in performances.
In the following years several other approaches have been used:

  - Genetic algorithms **SOURCE**
  - Simulated annealing **SOURCE**
  - Neural networks **SOURCE**

Sun et al. **SOUCE** find out that the left/right Bregman divergence is a major improvement for the whole algorithm in terms of performance.


## The code

Unfortunately, it doesn't look Python has a good library that includes the Sammon Mapping among its functions. If you know any, please comment!
The following code is _stolen_ from [Tom Pollard's repository](https://github.com/tompollard/sammon). Thanks.


{: .box-note}
**Note:** Gradient descent is shown to converge faster if applied on the PCA of the original space. As a result, starting the iterative process
from the PCA is a broadly accepted standard.



And here is the same code with syntax highlighting:

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

As you can see...

{: .box-warning}
**Warning:** Following Sammon's definition, if the distance between two points _i_ and _j_ is 0, the algorithm will try a division by 0.
Check for your data points to be **non repeated**, or your code will crash!

