---
title: Arithmetics between Pytorch tensor and Numpy array
description: >
  Python skills
---

Arithmetics between Pytorch tensor and Numpy array (without explicit casting) are not allowed.

For the following experiments:

PyTorch version: 1.2.0.dev20190611

Numpy version: 1.16.4


```
a = np.array([1, 6, 5])
b = torch.tensor([2, 8, 9])
print(a + b)

Out:
TypeError: add(): argument 'other' (position 1) must be Tensor, not numpy.ndarray
```

```
a = np.array([1, 6, 5])
b = torch.tensor([2, 8, 9])
print(b + a)

Out:
TypeError: add(): argument 'other' (position 1) must be Tensor, not numpy.ndarray
```


```
a = np.array([1, 6, 5])
b = torch.tensor([2, 8, 9])
print(a * b)

Out:
TypeError: mul(): argument 'other' (position 1) must be Tensor, not numpy.ndarray
```

```
a = np.array([1, 6, 5])
b = torch.tensor([2, 8, 9])
print(b * a)

Out:
TypeError: mul(): argument 'other' (position 1) must be Tensor, not numpy.ndarray
```

```
a = [1, 6, 5]
b = torch.tensor([2, 8, 9])
print(a * b)

Out:
TypeError: mul(): argument 'other' (position 1) must be Tensor, not list
```

```
a = 3
b = torch.tensor([2, 8, 9])
print(a * b)

Out:
tensor([ 6, 24, 27])
```

```
a = np.array([1, 6, 5])
b = torch.tensor([2, 8, 9])
print(a * b.numpy())

Out:
[ 2 48 45]
```

```
a = np.array([1, 6, 5])
b = torch.tensor([2, 8, 9])
print(torch.from_numpy(a) * b)

Out:
tensor([ 2, 48, 45])
```
