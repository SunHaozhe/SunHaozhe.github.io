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

Get the version

```zsh
conda --version
```

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


Get a list of all my Anaconda environments 

```zsh
conda info --envs
```

Create an Anaconda environment and install program(s)

```zsh
conda create -n env_name biopython
```

Activate the new Anaconda environment to use it 

```zsh
conda activate env_name
```

Deactivate the Anaconda environment

```zsh
conda deactivate 
```

Create a new Anaconda environment, specify Python version 

```zsh
conda create -n env_name python=3.4 

conda create -n python38 python=3.8 anaconda
```

Delete Anaconda environment

```zsh
conda env remove --name env_name
```


# Troubleshooter

* "Collecting package metadata" cannot proceed and never end #9221 [https://github.com/conda/conda/issues/9221](https://github.com/conda/conda/issues/9221)



# References 

* https://kapeli.com/cheat_sheets/Conda.docset/Contents/Resources/Documents/index 












































































