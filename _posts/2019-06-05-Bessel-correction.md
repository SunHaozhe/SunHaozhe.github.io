---
title: Bessel's correction
description: >
  Statistics
---

In statistics, Bessel's correction is the use of (n − 1) instead of (n) in the formula 
for the sample variance and sample standard deviation, where n is the number of 
observations in a sample. This method corrects the bias in the estimation of the 
population variance. It also partially corrects the bias in the estimation of the 
population standard deviation. However, the correction often increases the mean 
squared error in these estimations. 

An intuitive explanation of the source of bias from:

https://en.wikipedia.org/wiki/Bessel's_correction#Source_of_bias 

Is the estimate of the population variance that uses the sample mean always 
smaller than what we would get if we used the population mean? The answer is 
yes except when the sample mean happens to be the same as the population mean.

We are seeking the sum of squares of distances from the population mean, but end 
up calculating the sum of squares of differences from the sample mean, which, as will 
be seen, is the number that minimizes that sum of squares of distances. So unless the 
sample happens to have the same mean as the population, this estimate will always 
underestimate the sum of squared differences from the population mean.

************************************************************************************************************

https://en.wikipedia.org/wiki/Unbiased_estimation_of_standard_deviation

Bessel's correction only partially corrects the bias in the estimation of the 
population standard deviation because of Jensen's inequality (square root is a 
strictly concave function). Estimation of the population standard deviation (only) corrected by 
Bessel's correction (n - 1) introduces a negative bias (underestimation), i.e. Bessel's correction 
does not correct "enough" the bias. The unbiased estimation of standard deviation is a technically 
involved problem. It is not possible to find an estimate of the standard deviation which is 
unbiased for all population distributions, as the bias depends on the particular distribution. 
A rule of thumb for the normal distribution is to use (n − 1.5) instead of (n − 1) in the 
denominator. For statistical theory, it provides an exemplar problem in the context of 
estimation theory which is both simple to state and for which results cannot be obtained 
in closed form. It also provides an example where imposing the requirement for unbiased 
estimation might be seen as just adding inconvenience, with no real benefit. 





