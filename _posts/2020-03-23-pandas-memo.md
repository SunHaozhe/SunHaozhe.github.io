---
layout: post
category: Python
title: Pandas memo
tagline: by SunHaozhe
tags: 
  - Python
  - Pandas
  - API
  - Machine learning
mathjax: true
comments: true
published: true
---


Read dataset and reset index in place:

```python
train = pd.read_csv("train.csv")
train.set_index("id", inplace=True)
```

Visualize DataFrame:

```python
print(train.info())
train
```

Convert pandas column to DateTime:

```python
train['date'] =  pd.to_datetime(train['date'])
```

Convert object (string) columns to Categorical columns:

```python
categorical_cols = ["...", "..."]
train.loc[:, categorical_cols] = train.loc[:, categorical_cols].astype("category")
```































