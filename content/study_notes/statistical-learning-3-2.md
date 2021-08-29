---
title: 3.2 - Multiple Linear Regression
date: 2021-08-29 12:00:00
draft: false 
---

# Multiple Linear Regression

As in simple linear regression, estimates a response ``$Y$`` assuming  a linear relationship. In Multiple
linear regression, we are estimating the response using several predictors. The relationship takes form as:
`$$ Y = \beta_{0} + \beta_{1}X_{1} + \beta_{2}X_{2} + ... + \beta_{p}X_{p} + \epsilon$$`
The estimation of the parameters takes the same approach of simple linear regression,
minimizing the *sum of squared residuals* (RSS). 

> ### Correlation Between Predictors
> Suppose we have two predictors for a single response. If we were to compute two separate simple linear regressions,
> we might see that the two predictors have a statistically significant association with the response. In turn, 
> performing a multiple linear regression, we now see that only one of those have a statistically significant 
> coefficient.

> Why is that so? Probably due to the predictors being correlated. This is the case where one 'takes credit' for
> the other.


## Hypothesis Testing

In order to determine if there is a relationship between predictors and response, the framing of the
hypothesis is quite different. 

We need to check if *all* of the coefficients are zero (indicating that there is no relationship at all),
or that *at least one* coefficient is not null.


``$$ H_{0}: \beta_{1} = \beta_{2} = ... =  \beta_{p} = 0 $$``
``$$ H_{a}: \text{at least one }\beta_{j}\text{ is non-zero}$$``

This test can be answered by computing the *f-statistic*:

``$$ F =  \frac{(TSS - RSS)/p}{RSS/(n-p-1)}$$``

When there is no relationship, we expect F to take a value close to 1. On the other hand, if ``$H_{a}$``
is true, F would be larger than 1.


Why do we need to compute an *f-statistic* if we already have individual p-values? Well, when we have a large
amount of predictors, we are expected, by chance alone, to find some of them with small p-values.
The F-statistic adjusts for number of predictors, so it does not suffer from this problem.

## Deciding on Important Variables

Ideally, we would want to try a lot of different models, trying out each possible subset of our predictors,
and picking the best one based on some measurement of quality (Akaike Information Criterion, Bayesian Information Criterion,
``$R^{2}$`` etc.).

Only that there are a total of ``$2^{p}$`` possible models, which makes this approach only possible for small number
of predictors. Some classical approaches are:

### Forward Selection
Starting with the *null model* (a model containing only the intercept, and no predictors), we fit ``$p$`` simple
linear regressions and add to the *null model* the variable that results in the lowest RSS. We then repeat the
process, iteratively adding to the model variables until some stopping rule is met.

### Backward Selection
In opposition to the Forward Selection, we start with a model with all the variables, and remove the one with
the lowest *p-value*. The new ``$(p-1)$`` model is it, and the variable with the smallest *p-value* is removed.
This process is repeated until a stopping rule is met.

### Mixed Selection
A combination of Forward and Backward selection. Starting from the *null-model*, we add variables just as 
Forward Selection. Noting that the *p-values* change as we add more variables, if at some point the *p-value*
of one given variable drops below a certain amount, we remove it. 
We follow these steps until a stopping criterion is met.


## Model Fitness
Just as simple linear regression, we can assess model fitness using `$R^{2}$` and RSE.
We only have to be aware of a couple of things:

* The `$R^{2}$` measure will always increase when a variable is added to the model, even if this variable
is only weakly associated with the response.
This is due to the fact that adding another variable to the model allows us to fit to the data (the training
data, at least) better.

*  RSE is computed as:
`$$RSE = \sqrt{\frac{RSS}{(n-p-1)}}$$`
So models with more variables can have higher RSE if the decrease in RSS is small relative to the increase in ``$p$``.
