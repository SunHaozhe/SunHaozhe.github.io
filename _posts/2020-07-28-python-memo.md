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

Main file: 

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

Split strings:

```python
a = "This is Mike."
b = a.split() # ['This', 'is', 'Mike.']
```

```python
a = "Hello, my name is Mike, I am from Australia."
b = a.split(",") # ['Hello', ' my name is Mike', ' I am from Australia.'] 
```

File path:

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

Join:

```python
a = ["1", "2", "3", "4"]  
b = "-".join(a) # "1-2-3-4"
```

Pickle: 

```python
import pickle

# save_path ends with ".pkl"
with open(save_path, "wb") as f:
    pickle.dump(obj_, f)
    #pickle.dump(data, f, protocol=pickle.HIGHEST_PROTOCOL)

with open(save_path, "rb") as f:
    obj_ = pickle.load(f)
```


Reimport a module in python while interactive:

```python
import importlib
importlib.reload(module_name) 
```

Exception: 

```python
try:
    print(x)
except NameError:
    print("Variable x is not defined")
except:
    print("Something else went wrong")
```

```python
try:
    print(x) 
except Exception as e:
    print(e) 
```

```python
try:
    print("Hello")
except:
    print("Something went wrong")
else:
    print("Nothing went wrong")
```

```python
try:
    print(x)
except:
    print("Something went wrong")
finally:
    print("The 'try except' is finished")
```

```python
raise Exception("Blablabla")
```

Get object attributes in Python:

```python
dir(obj_)
```





















