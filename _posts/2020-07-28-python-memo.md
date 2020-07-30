---
layout: post
category: Python     
title: Python memo 
tagline: by SunHaozhe
tags: 
  - Python
  - API  
mathjax: true
comments: true
published: true
---



```python
if __name__ == "__main__":
    pass
```

Read file as a string:

```python
with open(file_path, "r") as file:
    content_as_str = file.read()
```

Read file line by line:

```python
# approach 1
with open(file_path, "r") as file:
    content = file.readlines()
content = [x.strip() for x in content] 

# approach 2 
with open(file_path, "r") as file:
    for line in file:
        print(line.strip()) 
```

Remove spaces at the beginning and at the end of the string:

```python
txt = "     d     "
x = txt.strip()
y = "abc" + x + "efg" # "abcdefg"
```

```python
os.curdir # '.'
os.pardir # '..'
os.sep # '/'
os.getcwd() # '/Users/ZZZ/Desktop/XXX/YYY'
```

```python
dir_path = os.path.join(XXX, YYY)
if not os.path.exists(dir_path):
    os.makedirs(dir_path)
```

```python
a = ["1", "2", "3", "4"]  
b = "-".join(a) # "1-2-3-4"
```

```python
import pickle

# save_path ends with ".pkl"
with open(save_path, "wb") as f:
    pickle.dump(obj_, f)
    #pickle.dump(data, f, protocol=pickle.HIGHEST_PROTOCOL)

with open(save_path, "rb") as f:
    obj_ = pickle.load(f)
```


Reimport a module in python while interactive

```python
import importlib
importlib.reload(module_name) 
```














