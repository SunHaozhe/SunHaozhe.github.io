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


