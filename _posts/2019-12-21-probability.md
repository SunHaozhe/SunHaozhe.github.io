---
layout: post
category: Mathematics
title: Probability
tagline: by SunHaozhe
tags: 
  - Mathematics
mathjax: true
comments: true
published: true
---



# Gaussian distribution

One-dimensional case:

$$\mathbb{P}_{\mu, \sigma}(x) = \frac{1}{\sqrt{2\pi \sigma^2}} \exp(-\frac{(x-\mu)^2}{2\sigma^2})$$

$d$-dimensional case:

$$\mathbb{P}_{\mu, \Sigma}(x) = \frac{1}{\sqrt{(2\pi)^d \det \Sigma}} \exp(-\frac{1}{2}(x-\mu)^\intercal \Sigma^{-1} (x-\mu))$$

# Laplace distribution

One-dimensional case:

$$\mathbb{P}_{\mu, b}(x) = \frac{1}{2b} \exp(-\frac{|x - \mu|}{b})$$

Mean: $\mu$

Variance: $2b^2$



# Chi-squared distribution

$\chi^2$ distribution with $k$ degrees of freedom is denoted by $\chi_k^2$. 

Mean: $k$

Variance: $2k$

Let $X_i \sim \mathcal{N}(0, 1)$, $X_i$'s are independent. $\overline{X} = \frac{1}{n} \sum_{i=1}^n X_i$.

$$\sum_{i=1}^n X_i^2 \sim \chi_n^2$$

$$\sum_{i=1}^n (X_i - \overline{X})^2 \sim \chi_{n-1}^2$$



# Student's t-distribution 

Let $X_i \sim \mathcal{N}(\mu, \sigma^2)$, $X_i$'s are i.i.d.. $\overline{X} = \frac{1}{n} \sum_{i=1}^n X_i$, $S^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \overline{X})^2$. 

$$\frac{\overline{X} - \mu}{\frac{\sigma}{\sqrt{n}}} \sim \mathcal{N}(0, 1)$$

$$t = \frac{\overline{X} - \mu}{\frac{S}{\sqrt{n}}} $$

$t$ follows Student's t-distribution with $n-1$ degrees of freedom. 

Mean: $0$ for $\nu > 1$ degrees of freedom, otherwise undefined  



# F-distribution

F-distribution with parameters $d_1$ and $d_2$ is denoted by $F(d_1, d_2)$.

If $X_1 \sim \chi_{d_1}^2$ and $X_2 \sim \chi_{d_2}^2$ are independent, then

$$\frac{\frac{X_1}{d_1}}{\frac{X_2}{d_2}} \sim F(d_1, d_2)$$





 