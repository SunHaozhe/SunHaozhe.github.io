---
layout: post
category: Python    
title: Translation of some technical terms 
tagline: by SunHaozhe
tags: 
  - Python 
  - API 
mathjax: true
comments: true
published: true
---

这篇文章还有问题，notebook用不成创建的虚拟环境 

To create a virtual environment: 

```python
# creates venv_X in the current directory 
virtualenv venv_X
```

To install the kernel for Jupyter notebook:

```python
# do this before activating the virtual environment
# 做完这一步之后不用激活虚拟环境，直接 jupyter notebook 就可以选虚拟环境对应的kernel
python3 -m ipykernel install --user --name=venv_X
```



To activate the virtual environment:

```python
source venv_X/bin/activate
```

To deactivate the virtual environment:

```python
deactivate
```

To delete the virtual environment:

```python
rm -r venv_X
```

To uninstall the kernel for Jupyter notebook:

```python
jupyter kernelspec uninstall venv_X
```

To see which kernels are available for Jupyter notebook:

```python
jupyter kernelspec list
```






