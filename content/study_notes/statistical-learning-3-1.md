---
title: 3 - Linear Regression
date: 2021-08-25 12:00:00
draft: false 
---

# Simple Linear Regression

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

## Assessing the Accuracy of the Coefficient Estimates

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

One thing to notice from the formulas: the more spread our data points are, the better our predictions for the coefficients (because 
`$\sum_{i=1}^{n}(x_{i} - \bar{x})^{2}$` will be greater, thus lowering the standard error).

In general, `$\sigma$` is not known but can be estimated from the data. This estimative is called the *residual standard error* (RSE):

`$$RSE = \sqrt{\frac{RSS}{(n-2)}}$$`


Standard errors are very useful for computing confidence intervals and for hypothesis testing

### Confidence Intervals

A confidence interval is a range of values that, given a certain probability, will hold the
true unknown value of the parameter in question. For example, a confidence interval of 95% 
means that, if we were to re-do this experiment 100 times, in only 5 of those, we would obtain
a value for the parameter that is outside of the interval.

For the simple linear regression, a confidence interval of 95% takes approximately the form:
``$$\hat{\beta_{1}} \pm 2SE(\hat{\beta_{1}})$$`` 
``$$\hat{\beta_{0}} \pm 2SE(\hat{\beta_{0}})$$`` 

### Hypothesis Testing

Standard errors are also used to compute hypothesis tests. The most common one is to test the null
hypothesis:

``$$ H_{0}: \beta_{1} = 0 \text{ (There is no relationship between X and Y)}$$``
``$$ H_{a}: \beta_{1} \ne 0 \text{ (There is some relationship between X and Y)}$$``

We are wondering, through this test, if we have enough evidence to be confident that ``$\beta_{1}$``
is non-zero (indicating that there is a relationship between our predictor and response). We need
to know if ``$\hat{\beta_{1}}$`` big enough to make that statement.

How large must it be? Well, it depends on ``$SE(\hat{\beta_{1}})$``. In practice, we compute a
*t-statistic*:
``$$ t = \frac{\hat{\beta_{1}} - 0}{SE(\hat{\beta_{1}})}$$``

That is, we want to compute how many standard deviations are we away from zero. We expect that ``$t$``
will follow a t-distribution with ``$n-2$`` degrees of freedom.

> Note that a t-distribution is used here because we don't know the population ``$\sigma$``. If we did,
> it would be safe to use a z-distribution. Here, actually, the population standard deviation is approximated
> by the sample deviation, i.e. the standard error.

Now, we can simply compute the probability of observing any number equal to ``$|t|$`` or larger,
assuming the null hypothesis is true. This probability is called *p-value*. A small p-value indicates
that it is unlikely to observe such a substantial association between ``$X$`` and ``$Y$`` due to chance
alone, in the absence of a *real* association.

## Assessing the Accuracy of the Model

There are a couple of ways we can get a sense of the extent our model fits the data, some of these
metrics are explained below.

### Residual Standard Error

The RSE is an estimate of the standard deviation of the error term ``$\epsilon$``. It can be interpreted
as the amount we expect the response will deviate from the regression line or, from a different
perspective, a lack of fit.

``$$ RSE =  \sqrt{ \frac{1}{n-2} RSS} $$``

The RSE is given in units of ``$Y$`` and so, it is not always clear what a good RSE is, as each 
model is going to be different.

### `$R^{2}$` Statistic

The `$R^{2}$` offers another measure of fitness, in the form of a proportion. It is the proportion
of the variance of the data explained by the model and ranges from 0 to 1. A value of 1 indicates
that the variable in question can fully explain the variances in the data.

``$$ R^{2} =  \frac{TSS - RSS}{TSS} $$``

Where, ``$ TSS =  \sum(y_{i} - \bar{y})^{2} $``
