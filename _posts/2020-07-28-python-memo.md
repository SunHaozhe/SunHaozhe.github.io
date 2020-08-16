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

Use `glob` to find all the path names matching a specified pattern according to the rules used by the Unix shell: 

```python
import glob

for file_name in glob.glob(os.path.join("XXX", "*.txt")):
    print(file_name) 

# File names in the above code are not sorted. 
# If needed, use the following:

for file_name in sorted(glob.glob(os.path.join("XXX", "*.txt")), key=lambda x: TODO):
    print(file_name) 
    
# To search file names in subdirectories:

for file_name in glob.glob(os.path.join("XXX", "*/*.txt")):
    print(file_name) 
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

Sorting:

```python
a = [2, 8, 1, 4, 3, 9, 7]
print(a)

b = sorted(a)                # ascending order 
c = sorted(a, reverse=True)  # descending order

print(a)
print(b)
print(c)
```

```
[2, 8, 1, 4, 3, 9, 7]
[2, 8, 1, 4, 3, 9, 7]
[1, 2, 3, 4, 7, 8, 9]
[9, 8, 7, 4, 3, 2, 1]
```

```python
a = ["cccc", "b", "dd", "aaa"] 
sorted(a)           # ['aaa', 'b', 'cccc', 'dd']
sorted(a, key=len)  # ['b', 'dd', 'aaa', 'cccc']
```

```python
def func(x): 
    return x % 7
  
a = [15, 3, 11, 7] 
sorted(a)            # [3, 7, 11, 15]
sorted(a, key=func)  # [7, 15, 3, 11]
```

```python
a = [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]

b = sorted(a, key=lambda x: x[2]) 
```

```
[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
```

```python
import operator 

a = [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]

b = sorted(a, key=operator.itemgetter(2)) 
```

```
[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)] 
```

```python
a = {"Allen": 3, "Tom": 5, "John": 0, "Bob": -2}

# sort dict by key 
b = sorted(a)             # ['Allen', 'Bob', 'John', 'Tom']

# sort dict by value 
c = sorted(a, key=a.get)  # ['Bob', 'John', 'Allen', 'Tom'] 
```

Dict comprehension to reverse key-value pair in a dictionary: 

```python
id2word = {v: k for k, v in word2id.items()} 
```




































