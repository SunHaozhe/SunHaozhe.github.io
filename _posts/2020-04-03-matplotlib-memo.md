---
layout: post
category: Python
title: Matplotlib memo 
tagline: by SunHaozhe
tags: 
  - Python
  - API
mathjax: true
comments: true
published: true
---

`matplotlib` is a plotting library for the Python programming language and its numerical mathematics extension `numpy`. `matplotlib.pyplot` provides a MATLAB-like plotting framework. `pylab` combines `pyplot` with `numpy` into a single namespace. `pylab` is now discouraged. [1, 2, 3]

```python
import matplotlib.pyplot as plt
```

```python
params = {'legend.fontsize': 'xx-large',
         'axes.labelsize': 'xx-large',
         'axes.titlesize':'xx-large',
         'xtick.labelsize':'xx-large',
         'ytick.labelsize':'xx-large'}
plt.rcParams.update(params)
```





# References

[1] Matplotlib. (2005, October 14). Wikipedia, the free encyclopedia. Retrieved April 3, 2020, from https://en.wikipedia.org/wiki/Matplotlib

[2] Pyplot — Matplotlib 2.0.2 documentation. (n.d.). Matplotlib: Python plotting — Matplotlib 3.2.1 documentation. https://matplotlib.org/api/pyplot_api.html

[3] Matplotlib, Pyplot, Pylab etc: What's the difference between these and when to use each? (2019, August 31). queirozf.com. https://queirozf.com/entries/matplotlib-pylab-pyplot-etc-what-s-the-different-between-these





















