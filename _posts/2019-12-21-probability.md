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

