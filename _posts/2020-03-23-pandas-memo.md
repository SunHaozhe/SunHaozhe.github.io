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

Convert object (string) columns to Categorical columns:

```python
categorical_cols = ["...", "...", "..."]
train_df.loc[:, categorical_cols] = train_df.loc[:, categorical_cols].astype("category")
```

Convert Categorical columns into dummy columns:

```python
train_df = pd.get_dummies(train_df, drop_first=True)
# drop_first: whether to get k-1 dummies out of k categorical 
# levels by removing the first level.

train_df = pd.get_dummies(train_df, columns=["...", "..."])
# If columns is None (default) then all the columns with 
# object or category dtype will be converted.
```

Fill missing values:

```python
train_df["name"].fillna("unknown", inplace=True)
train_df["age"].fillna(train_df["age"].mean(), inplace=True)
train_df["A"].fillna(method="ffill", inplace=True)
```

Remove missing values:

```python
train_df.dropna(axis=0, how="any", inplace=True) # drop rows
train_df.dropna(axis=1, how="any", inplace=True) # drop columns
```

Remove columns/features:

```python
train_df.drop(["...", "...", "..."], axis=1, inplace=True)
```

Add interaction term:

```python
train_df["C"] = train_df["A"] * train_df["B"]
```

Reset the index to the default integer index:

```python
train_df.reset_index(inplace=True) # the old index is added as a column
train_df.reset_index(drop=True, inplace=True) # drop the old index 
```

Convert pandas column to DateTime:

```python
train_df["date"] =  pd.to_datetime(train_df["date"])
```

Select rows between two dates:

```python
train_df.loc[(train_df["date"] >= "2020-03-17") & (train_df["date"] < "2020-03-20"), :]
```

Select rows if value in column is in a list of values:

```python
train_df.loc[train_df["country"].isin(["China", "France"]), :]

# to get the opposite, use ~
train_df.loc[~train_df["country"].isin(["China", "France"]), :]
```

Normalize features:

```python
# normalize features to a given range
from sklearn.preprocessing import MinMaxScaler
# normalize features by removing the mean and scaling to unit variance
from sklearn.preprocessing import StandardScaler

scaler = MinMaxScaler() # StandardScaler()
# Let's assume train_df has not been augmented 
# by the constant column yet.
train_df = pd.DataFrame(scaler.fit_transform(train_df), 
columns=train_df.columns, index=train_df.index)
train_df = train_df.assign(const=1)
```

Split features `X` and labels `y`:

```python
y_train = train_df.loc[:, "y"]
X_train = train_df.drop("y", axis=1)
```

Split training set and test set:

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, 
test_size=0.3, random_state=42)

```

Add a column of constant `1`'s:
```python
X_train = X_train.assign(const=1)
# Used for statsmodels
# The added column's name is "const"
```

Visualize the number of distinct values that each feature can take:

```python
train_df.nunique()
```

Visualize the number of distinct values that each feature can take and the corresponding data type:

```python
unique_counts = pd.DataFrame([(col, train_df[col].dtype, train_df[col].nunique()) \
for col in train_df.columns], columns=["col_name", "dtype", "nunique"])\
.set_index("col_name").sort_values(by=['nunique'])
unique_counts
```

Visualize counts of unique values in descending order of frequency:

```python
train_df["A"].value_counts()
```

For a certain column, parse string representations to lists of elements:

```python
import ast
col_names = ["genres", "spoken_languages"]
for col in col_names:
    train_df[col] = train_df[col].apply(lambda x: ast.literal_eval(x)) 
```

For a certain column, convert lists of strings to dummies: 

```python
for col in ["genres", "production_countries", "spoken_languages"]:
    train_df = train_df.join(train_df[col].str.join('|').str.get_dummies()\
    .add_prefix(col + "_")).drop(col, axis=1)
```

```
genres: [Comedy, Drama, Family, Romance], [Drama, Thriller], ...	
genres_Comedy, genres_Drama, genres_Family, genres_Romance, ...
```

Get a subset of the DataFrame’s columns based on the column dtypes:

```python
train_df.select_dtypes(include=["object", "bool", "float64", "int"])
```

Make a histogram:

```python
train_df["age"].hist(bins=10)
plt.show()
```
















