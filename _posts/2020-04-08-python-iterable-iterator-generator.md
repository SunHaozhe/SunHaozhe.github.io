---
layout: post
category: Python
title: Python iterable iterator generator
tagline: by SunHaozhe
tags: 
  - Python
  - API
mathjax: true
comments: true
published: true
---


Iterable: 

* It is an object that contains a countable number of values. 
* It is an object that can be iterated upon, meaning that you can traverse through all the values.
* It is an object that has an `__iter__()` method or defines a `__getitem__()` method. 
* It generates an Iterator when passed to `iter()` method.


Iterator:

* It is an object which is used to iterate over an iterable object. 
* it must implement `__iter__()`method and `__next__()`method. 
* `__next__()` method returns the next item of the object.
* It is an object with state that remembers where it is during iteration. 
* It is self-iterable (meaning that it has an `__iter__` method that returns `self``. 



Every iterator is also an iterable, but not every iterable is an iterator. For example, a list is iterable but it is not an iterator. 

$$\text{iterator} \subsetneq \text{iterable}$$

When a `for` loop is executed, the `for` statement calls `iter()` on the iterable object. If successful, the `iter()` call will return an iterator object that defines the `__next__()` method, which accesses elements of the object one at a time. The `__next__()` method will raise a `StopIteration` exception, if there are no further elements available. The `for` loop will terminate as soon as it catches a `StopIteration` exception. 

```python
list_ = ["A", "B", "C"] 
iterator_obj = iter(list_) 
print(next(iterator_obj)) # A
print(next(iterator_obj)) # B
print(next(iterator_obj)) # C
```


# References

[1] Python | Difference between iterable and iterator. (2019, August 23). GeeksforGeeks. https://www.geeksforgeeks.org/python-difference-iterable-iterator/

[2] Python Iterators. (n.d.). W3Schools Online Web Tutorials. https://www.w3schools.com/python/python_iterators.asp

[3] Glossary — Python 3.8.2 documentation. (n.d.). 3.8.2 Documentation. https://docs.python.org/3/glossary.html

[4] What exactly are iterator, iterable, and iteration? (n.d.). Stack Overflow. https://stackoverflow.com/questions/9884132/what-exactly-are-iterator-iterable-and-iteration

[5] Python Iterators (__iter__ and __next__): How to use it and why? (n.d.). Programiz: Learn to Code for Free. https://www.programiz.com/python-programming/iterator




























