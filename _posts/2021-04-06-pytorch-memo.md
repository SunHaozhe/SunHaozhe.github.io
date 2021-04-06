---
layout: post
category: Python     
title: PyTorch memo 
tagline: by SunHaozhe
tags: 
  - memo
  - PyTorch
  - Python
mathjax: true
comments: true
published: true
---

# Imports

```python
import torch 
import torch.nn as nn
import torch.nn.functional as F  
```


# Initialization 

Returns a `torch.Tensor` filled with random numbers from a normal distribution with mean 0 and variance 1 (also called the standard normal distribution)

```python
# By default, requires_grad == False 
torch.randn(2, 3)
# or equivalently
torch.randn((2, 3))
```

```
tensor([[ 1.5954,  2.8929, -1.0923],
        [ 1.1719, -0.4709, -0.1996]])
```

Please note the difference between `torch.Tensor` and `torch.nn.parameter.Parameter` (`nn.Parameter(torch.randn(2, 3))`, by default `requires_grad == True`).





































































