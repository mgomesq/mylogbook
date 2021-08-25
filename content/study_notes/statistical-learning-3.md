---
title: 3 - Linear Regression
date: 2021-08-25 12:00:00
draft: true 
---

## Simple Linear Regression

Simple linear regression estimates a `$Y$` response using one predictor `$X$`, assuming that the relationship between them takes form as:
`$$ Y = \beta_{0} + \beta_{1}X$$`
Now, `$\beta_{0}$` and `$\beta_{1}$` are constants that represent the *intercept* and *slope* of the linear model.
In order to obtain their estimates, `$\hat{\beta_{0}}$` and `$\hat{\beta_{1}}$`, using a set of `$n$` observations,
`$(x_{1}, y_{1}), (x_{2}, y_{2}), ..., (x_{n}, y_{n})$`, one has to choose the parameters such that `$y_{i} \approx \hat{y}_{i}$` for every
observation.

In practical terms, you try to minimize a cost function (one that penalizes wrong predictions). It is customary to choose to minimize the
residual sum of squares (RSS) for this task.

We define the residual sum of squares as
`$$ RSS = e_{1}^{2},e_{2}^{2} +...+ e_{n}^{2}$$`

### Assessing the Accuracy of the Coefficient Estimates

Once the coefficients are obtained, it is possible to draw a *least squares line*, which is the line that best fits the observations we have. 
It is important to note that, the least squares line **is not** the actual **true** relationship line (called *population regression line*), but
only an estimate of it. If we were to draw a different sample of the population and redo the regression, we would get a different set of coefficients
and another *least squares line*.

Now, `$\beta_{0}$` and `$\beta_{1}$` hold a nice property in linear regression: they are *unbiased* estimators. Which is to say, if we were
to draw a different sample and compute the coefficients over and over again, on average these coefficients would be exactly equal to the **true**
ones. We might get it wrong each time, but we do not systematically over - or under - estimate them.

We usually can't draw as many samples as we want. Often the dataset we get is the one we have to work with.
So a natural question to make is: how far off will my single estimate of the parameters be?

To answer this question, we can calculate the **standard error** of `$\hat{\beta_{0}}$` and `$\hat{\beta_{1}}$`.
`$$var(\hat{\beta}) = SE(\hat{\beta})^{2}$$`
The standard error, `$SE(\hat{\beta})$` tell us the average amount that a single prediction differs from the true value of `$\beta$`.

`$$ SE(\hat{\beta_{0}})^{2} = \sigma^{2} \left [ \frac{1}{n} + \frac{\bar{x}^{2}}{\sum_{i=1}^{n}(x_{i} - \bar{x})^{2}}\right ] $$`

`$$ SE(\hat{\beta_{1}})^{2} = \frac{\sigma^{2}}{\sum_{i=1}^{n}(x_{i} - \bar{x})^{2}}$$`
> *For these formulas to be valid, the errors should be Gaussian, uncorrelated and have common variance `$\sigma^{2}$`.*

One thing to notice from the formulas: the more spread our data points are, the better our predictions for the coefficients are (because 
`$\sum_{i=1}^{n}(x_{i} - \bar{x})^{2}$` will be greater, thus lowering the standard error).

In general, is not known but can be estimated from the data. This estimative is called the *residual standard error* (RSE):

`$$RSE = \sqrt{\frac{RSS}{(n-2)}}$$`


___Standard errors can be used to compute confidence intervals


### Assessing the Accuracy of the Model
