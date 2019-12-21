---
layout: post
category: Mathematics
title: Machine Learning quick notes
tagline: by SunHaozhe
tags: 
  - Mathematics
  - Machine learning
mathjax: true
published: true
---

By convention, $X \in \mathbb{R}^{n\times p}$ where $n$ denotes the number of samples, $p$ denotes the number of features.



************************************************************************************************

# PCA

Recall SVD, for any matrix $X\in \mathbb{R}^{n\times p}$,

$$X = U\Sigma V^\intercal$$

where $U\in \mathbb{R}^{n\times n}$, $V \in \mathbb{R}^{p\times p}$, $V^\intercal$ is the transpose of $V$. The columns of $U$ are called left singular vectors, the columns of $V$ are called right singular vectors. $U$ and $V$ are orthogonal matrices. 

To compute PCA for $X\in \mathbb{R}^{n\times p}$, 

* For each column/feature of $X$, substract the mean. Optionally, one can also divide the standard deviation for each column, this seems to be recommended. Call the resulted matrix $\tilde{X}\in \mathbb{R}^{n\times p}$. 
* Compute SVD of $\tilde{X}$, one obtains $\tilde{X} = U\Sigma V^\intercal$. The columns of $V$ (right singular vectors) are called principal components. Equivalently, this is to compute eigendecomposition of $\tilde{X}^\intercal \tilde{X} \in \mathbb{R}^{p\times p}$. $\tilde{X}^\intercal \tilde{X}$ is the empirical covariance matrix between features up to a normalization constant. The right singular vectors  are the eigenvectors of $\tilde{X}^\intercal \tilde{X}$. That is, $\tilde{X}^\intercal \tilde{X} = V S V^\intercal = V S V^{-1}$. By convention, the singular values are sorted in descending order, singular vectors are sorted accordingly.
* $X^* = \tilde{X} V = U\Sigma \in \mathbb{R}^{n\times p}$ is the transformed version of $X$ by PCA. So far, one uses a new orthogonal basis to represent data $X$. If one seeks for dimensionality reduction, one keeps only the $k$ principal components which correspond to the $k$ largest singular values. That is, $V_k \in \mathbb{R}^{p\times k}$, $X_k^* = \tilde{X} V_k \in \mathbb{R}^{n\times k}$. 
* For unseen test data $Z\in \mathbb{R}^{m\times p}$, normalize it with the statistics (means, standard deviations) of training set and then do the matrix multiplication $Z_k^* = \tilde{Z}V_k \in \mathbb{R}^{m\times k}$. One should neither use statistics of test set to normalize nor compute the statistics using the whole dataset (training + test). The principal components are of course those computed from training set. 



************************************************************************************************
