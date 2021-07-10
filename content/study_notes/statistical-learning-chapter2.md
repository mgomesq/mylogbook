---
title: Chapter 2 - What Is Statistical Learning?
date: 2021-07-10 17:51:42
draft: true
---

The second chapter offers us a good overview on the prediction of a given quantity Y.
It touches on key concepts of Machine Learning and sets the tone of the book.

## What is Statistical Learning?

Well, suppose we want to predict [House Sale Prices](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/overview) using data you've gathered.
It is customary to call the variable you want to predict`$Y$`and the set of features used for predictions `$X$`.

Mathematically, what we want is to find a function of`$X$`,`$f(X)$`that fully describes house prices. This function represents all
of the information we can learn from `$X$`about`$Y$`.

What happens in practice, is that the prediction of`$Y$` comes with a random error denoted by`$\epsilon$`.
`$$ Y = f(X) + \epsilon $$`
This error has a mean equal to zero and is independent of`$X$`. We'll talk about it later on.

Statistical learning is, at its essence, a series of techniques that are used to estimate`$f$`.

## Prediction/Inference

We often want to estimate`$f$`for two reasons **prediction and inference**

`$ \hat{Y} = \hat{f}(X) $`

