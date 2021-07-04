---
layout: post
category: Misc     
title: Number of trainable parameters of neural networks in torchvision.models
tagline: by SunHaozhe
tags: 
  - PyTorch
  - Machine learning
mathjax: true
comments: true
published: true
---

```bash
                 model  nb_trainable_parameters nb_trainable_parameters_human_readable
15       squeezenet1_1                  1235496                                  1.24M
14       squeezenet1_0                  1248424                                  1.25M
22  shufflenet_v2_x0_5                  1366792                                  1.37M
33          mnasnet0_5                  2218512                                  2.22M
23  shufflenet_v2_x1_0                  2278604                                  2.28M
28  mobilenet_v3_small                  2542856                                  2.54M
34         mnasnet0_75                  3170208                                  3.17M
24  shufflenet_v2_x1_5                  3503624                                   3.5M
26        mobilenet_v2                  3504872                                   3.5M
35          mnasnet1_0                  4383312                                  4.38M
27  mobilenet_v3_large                  5483032                                  5.48M
36          mnasnet1_3                  6282256                                  6.28M
25  shufflenet_v2_x2_0                  7393996                                  7.39M
16         densenet121                  7978856                                  7.98M
9             resnet18                 11689512                                 11.69M
21           googlenet                 13004888                                    13M
17         densenet169                 14149480                                 14.15M
19         densenet201                 20013928                                 20.01M
10            resnet34                 21797672                                  21.8M
29     resnext50_32x4d                 25028904                                 25.03M
11            resnet50                 25557032                                 25.56M
20        inception_v3                 27161264                                 27.16M
18         densenet161                 28681000                                 28.68M
12           resnet101                 44549160                                 44.55M
13           resnet152                 60192808                                 60.19M
0              alexnet                 61100840                                  61.1M
31     wide_resnet50_2                 68883240                                 68.88M
30    resnext101_32x8d                 88791336                                 88.79M
32    wide_resnet101_2                126886696                                126.89M
1                vgg11                132863336                                132.86M
2             vgg11_bn                132868840                                132.87M
3                vgg13                133047848                                133.05M
4             vgg13_bn                133053736                                133.05M
5                vgg16                138357544                                138.36M
6             vgg16_bn                138365992                                138.37M
7                vgg19                143667240                                143.67M
8             vgg19_bn                143678248                                143.68M
```

Source code:

```python
"""
MIT License

Copyright (c) 2021 Haozhe Sun

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


https://pytorch.org/vision/stable/models.html
"""

import pandas as pd
import torch 
import torch.nn as nn
import torch.nn.functional as F  
import torchvision

# human readable large numbers
from millify import millify

def get_nb_trainable_parameters(model):
    return sum([x.numel() for x in model.parameters() if x.requires_grad])


model_names = ["alexnet",
               "vgg11",
               "vgg11_bn",
               "vgg13",
               "vgg13_bn",
               "vgg16",
               "vgg16_bn",
               "vgg19",
               "vgg19_bn",
               "resnet18",
               "resnet34",
               "resnet50",
               "resnet101",
               "resnet152",
               "squeezenet1_0",
               "squeezenet1_1",
               "densenet121",
               "densenet169",
               "densenet161",
               "densenet201",
               "inception_v3",
               "googlenet",
               "shufflenet_v2_x0_5",
               "shufflenet_v2_x1_0",
               "shufflenet_v2_x1_5",
               "shufflenet_v2_x2_0",
               "mobilenet_v2",
               "mobilenet_v3_large",
               "mobilenet_v3_small",
               "resnext50_32x4d",
               "resnext101_32x8d",
               "wide_resnet50_2",
               "wide_resnet101_2",
               "mnasnet0_5",
               "mnasnet0_75",
               "mnasnet1_0",
               "mnasnet1_3"]

model_strings = []
for model_name in model_names:
    model_strings.append((model_name, "torchvision.models." + model_name + "(pretrained=False)"))

df = []
for model_name, model_string in model_strings:
    model = eval(model_string)
    nb_params = get_nb_trainable_parameters(model)
    df.append((model_name, nb_params))
df = pd.DataFrame(df, columns=["model", "nb_trainable_parameters"])
df["nb_trainable_parameters_human_readable"] = df["nb_trainable_parameters"].apply(lambda x: millify(x, precision=2))
df.sort_values("nb_trainable_parameters", ascending=True, inplace=True, axis=0)

pd.set_option('display.max_rows', None)
print(df)
```

