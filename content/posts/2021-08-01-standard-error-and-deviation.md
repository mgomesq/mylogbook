---
title: Standard Deviation and Standard Error
date: 2021-08-01 17:51:42
cover:
    image: "/img/std_se/se_1.png"
    relative: false # To use relative path for cover image, used in hugo Page-bundles
tags:
- Statistics
- Standard Deviation 
- Standard Error
- Study Notes
categories:
- Study Notes
keywords:
    - Statistics
    - Standard Deviation 
    - Standard Error
    - Study Notes
draft: false
---

Recently I've been caught up on understanding the differences between two measurements of 
spread: Standard Deviation and Standard Error. 
Trying to understand when to use one or another on hypothesis testing has led me down the rabbit hole 
of which I managed to get out.


## Standard Deviation

Suppose you have a sample, this sample contains ``$n$`` measurements of a given variable. This measurements
are not always the same as they vary a little around some mean value, denoted by ``$\mu$``.

*A measurement of 
spread of a sampling distribution is given by the standard deviation ``$\sigma$``*.

``$$\sigma = \sqrt{\frac{1}{N}\sum_{i=0}^{N}(x_{i} - \mu)^{2}}$$``

## Standard Error

If you were to repeat this experiment, taking ``$n$`` measurements each time and recording the results,
you would likely get different results. This measurements come from a random variable and so, the mean
value obtained is also prone to variation.

{{< figure src="/img/std_se/se_2.png" >}}

The thing is, you don't need to repeat a lot of experiments to estimate the 
variation of the mean *(as proven below)*. 
*A measurement of the spread of the estimates of ``$\mu$`` from a sampling distribution is given by the
standard error ``$\sigma_{\bar{x}}$``* - a fancy name for standard deviation of the mean -
and can be calculated as:

``$$\sigma_{\bar{x}} = \frac{\sigma}{\sqrt{n}}$$``

> Here, it is important to note that the variation of the population often can be approximated
> as the standard deviation of the sample, ``$\sigma = \sigma_{sample}$``.

{{< figure src="/img/std_se/proof_SE.png" >}}

## Conclusion

Standard deviation and standard error are measures of different things.
When computing a hypothesis test, you have to understand which one you need to use,
and that's on a case-by-case basis.

**The standard deviation** measures variability of individual observations, and can be
used to test if a given measure is part of a distribution or not.

**The standard error** measures variability in estimates of parameters. It should
be used, for example, if the hypothesis test involves *mean*.

A use case for it would be: A box contains a lot of numbered values.
You say that the mean of these values in the box is 50 *(the null hypothesis)*,
so you take 25 measures from the box and find that the sample you took has mean 48
with standard deviation 2. Is this sample mean evidence that the population mean
is different than 50? *(alternative hypothesis)*. Then you should divide the sample
standard deviation by the square root of 2 and compute the hypothesis test.
