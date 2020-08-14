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




# seaborn

For `seaborn` version `0.10.1`, 

```python
# This import will not change the style for the rest of the session
import seaborn

# This command will change the style for the rest of the session  
seaborn.set()

# This command will restore the style  
seaborn.reset_orig()
```

One can use the style context manager which sets a style temporarily:

```python
style_name = "seaborn-darkgrid"

with plt.style.context(style_name):
    pass 
```

Valid style names include: `"seaborn-darkgrid"`, `"seaborn-whitegrid"`, `"seaborn-dark"`, `"seaborn-white"`, `"seaborn-ticks"`, `"seaborn-bright"`, `"seaborn-colorblind"`, `"seaborn-dark-palette"`, `"seaborn-paper"`, `"seaborn-poster"`, `"seaborn-talk"`, `"bmh"`, `"classic"`, `"dark_background"`, `"fivethirtyeight"`, `"ggplot"`, `"grayscale"`, etc.



# References


[1] Matplotlib. (2005, October 14). Wikipedia, the free encyclopedia. Retrieved April 3, 2020, from https://en.wikipedia.org/wiki/Matplotlib

[2] Pyplot — Matplotlib 2.0.2 documentation. (n.d.). Matplotlib: Python plotting — Matplotlib 3.2.1 documentation. https://matplotlib.org/api/pyplot_api.html

[3] Matplotlib, Pyplot, Pylab etc: What's the difference between these and when to use each? (2019, August 31). queirozf.com. https://queirozf.com/entries/matplotlib-pylab-pyplot-etc-what-s-the-different-between-thes`
























