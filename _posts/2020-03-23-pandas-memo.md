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
train_df = pd.read_csv("train.csv")
train_df.set_index("id", inplace=True)
```

Visualize DataFrame:

```python
print(train_df.info())
train_df
```

Convert pandas column to DateTime:

```python
train_df["date"] =  pd.to_datetime(train_df["date"])
```

Convert object (string) columns to Categorical columns:

```python
categorical_cols = ["...", "...", "..."]
train_df.loc[:, categorical_cols] = train_df.loc[:, categorical_cols].astype("category")
```

Convert Categorical columns into dummy columns:

```python
train_df = pd.get_dummies(train_df, drop_first=True)
# drop_first: whether to get k-1 dummies out of k categorical levels by removing the first level.
```

Remove missing values:

```python
train_df.dropna(axis=0, how="any", inplace=True) # drop rows
train_df.dropna(axis=1, how="any", inplace=True) # drop columns
```

Remove columns/features:

```python
X_train.drop(["...", "...", "..."], axis=1, inplace=True)
```

Reset the index to the default integer index:

```python
train_df.reset_index(inplace=True) # the old index is added as a column
train_df.reset_index(drop=True, inplace=True) # drop the old index 
```


Split features `X` and labels `y`:

```python
y_train = train_df.loc[:, "y"]
X_train = train_df.drop("y", axis=1)
```


























