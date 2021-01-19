---
layout: post
category: Misc     
title: Anaconda memo 
tagline: by SunHaozhe
tags: 
  - memo
mathjax: true
comments: true
published: true
---

# Managing Conda and Anaconda 

Verify conda is installed, check version

```zsh
conda info
```

Update conda package and environment manager

```zsh
conda update conda
```

Update the anaconda meta package

```zsh
conda update anaconda
```

# Managing Environments


Get a list of all my environments, active environment shown with `

```zsh
conda info --envs
```

Create an environment and install program(s)

```zsh
conda create -n snowflakes biopython
```

Activate the new environment to use it 

```zsh
conda activate snowflakes
```

Deactivate the environment

```zsh
conda deactivate 
```

Create a new environment, specify Python version 

```zsh
conda create -n bunnies python=3.4 astroid 
```



# Troubleshooter

* "Collecting package metadata" cannot proceed and never end #9221 [https://github.com/conda/conda/issues/9221](https://github.com/conda/conda/issues/9221)



# References 

* https://kapeli.com/cheat_sheets/Conda.docset/Contents/Resources/Documents/index 












































































