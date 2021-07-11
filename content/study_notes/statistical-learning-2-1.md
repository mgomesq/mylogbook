---
title: 2.1 - What Is Statistical Learning?
date: 2021-07-10 17:51:42
draft: false
---

The second chapter offers us a good overview on the prediction of a given quantity Y.
It touches on key concepts of Machine Learning and sets the tone of the book.

## What is Statistical Learning?

Well, suppose we want to predict [House Sale Prices](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/overview) using data you've gathered.
It is customary to call the variable you want to predict`$Y$`and the set of features`$X$`.

Mathematically, what we usually want is to find a function of`$X$`,`$f(X)$`that fully describes house prices. This function represents all
of the information we can learn from`$X$`about`$Y$`.

 learning is, at its essence, a series of techniques that are used to estimate`$f$`.

## Prediction/Inference

We often want to estimate`$f$`for two reasons **prediction and/or inference**

### Prediction  

In prediction, the goal is to provide, given a set of predictors (features, inputs etc.)`$X$`, an accurate estimate of`$Y$`.
`$$ \hat{Y} = \hat{f}(X) $$`

The accuracy of the prediction is tied to two quantities, called *reducible error* and *irreducible error*

What happens in practice is that the prediction of`$Y$` comes with a random error denoted by`$\epsilon$`.
`$$ Y = f(X) + \epsilon $$`
This error has a mean equal to zero and is independent of`$X$`.

In general,`$\hat{f}$`will not be a perfect estimate of`$f$`, which leads to a *reducible error*. This error can be attenuated
by improving the data or the technique used for the statistical learning.
On the other hand, even if we estimate with perfection`$f$`, we would still see some error in our predictions. This is because`$Y$` is also 
a function of`$\epsilon$`, which is, by definition, independent of`$X$`. This irreducible error is larger than zero because it may
contain unmeasured variables that are useful for predicting`$Y$`. For example, the price a house is sold also depends of the well-being of the
buyer on the day the sale was made.

### Inference

In inference, we are interested in, given a set of predictors and responses, understanding the relationships between`$X_{1}, X_{2}... X_{p}$`and`$Y$`.
The questions that arise are: Which predictors are associated with the response? What is the relationship between each predictor and the response?


## How do We Estimate`$f$`?

It is applied a statistical learning method to a training data, in order to find a function`$\hat{f}$`such that`$Y \approx \hat{f}(X)$` for any observation.

Generally speaking, the methods for estimating`$f$` can be classified as

* Parametric/ Non-Parametric
* Supervised/ Unsupervised
* Regression/ Classification


### Parametric/ Non-Parametric

Parametric methods involve a two step approach:
1. Assume a shape of`$f$`
2. Use training data to fit`$f$`

This method reduces the problem of estimating`$Y$` to a problem of finding the best parameters to fit`$f$`. It reduces the complexity
of trying to fit an arbitrary function, but the model we choose will usually not match the unknown form of`$f$`.

We can avoid the simplification involved in assuming a shape, by choosing to use a non-parametric method, where we do not make explicit assumptions
about the functional form of`$f$`. Instead, they seek an estimate of`$f$` that fits to the data, but not so much as to over-fit. This approach has a downside
of requiring a lot of data to produce a good estimate.

### Supervised/ Unsupervised

Supervised methods are those where, for each observation of the predictors, we have a observation of the response. These are methods that use
*labeled data*. On the other hand, unsupervised methods operate in settings where we do not have a observation of the response, that is, when
we have *unlabeled data*.

### Regression/ Classification

These methods differ in the format of the observed response. These variables can either be *quantitative* or *qualitative*.
Problems with a continuous response are named regression problems, and when the response is categorical, we say it is a qualitative problem.

