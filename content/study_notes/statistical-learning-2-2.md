---
title: 2.2 - Acessing Model Accuracy
date: 2021-07-11 12:00:00
draft: false
---

In order to evaluate the performance of a model we need to, in some way, measure
how closely our predictions come to the observed data.

## Mean Squared Error (MSE)
In regression problems, the most common metric used for evaluating performance is the Mean Squared Error, defined as:
`$$ MSE = \frac{1}{n}\sum_{i=1}^{n}(y_{i}-\hat{f}(x_{i}))^2$$`
The MSE is computed for the training data in order to adjust the fit of the created model. But in reality, we do not
care about the MSE for the training data! We want to see how the model performs in *unseen data*.

That is, we want to choose a model that gives the lowest *test MSE*. Which is not that trivial. There is no way to guarantee that
a model that perfomrs well in the *training data* will have a good performance in *test data*. 

Different models that have different flexibility (*degrees of freedom*, I mean) will provide different MSE for *training* and *testing* data.

As the flexibility of the statistical learning method increases, it is observed a monotone decrease in the *training MSE* and a U-shape increase in *test MSE*.
This is a **fundamental property** that holds regardless of the data that is used.

When the method provides us a small *traing MSE* and a large *test MSE* it is often the case that *overfitting* is happening.
In this case, the fitting follows to closely the error in the *traing data*, finding patterns and extending them to the *test data*, where they simply
don't exist.


## Bias-variance Trade Off
(...)
