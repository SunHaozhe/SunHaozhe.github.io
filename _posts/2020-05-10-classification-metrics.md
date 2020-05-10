---
layout: post
category: Mathematics
title: Classification metrics
tagline: by SunHaozhe
tags: 
  - Common knowledge
  - Mathematics
  - Machine learning
mathjax: true
comments: true
published: true
---


* true positive (TP) 
* true negative (TN)
* false positive (FP)
    * type I error: rejection of a true null hypothesis
* false negative (FN) 
    * type II error: non-rejection of a false null hypothesis 


Confusion matrix:

| | |
|-|-|
| TP                 | FP (type I error) |
| FN (type II error) | TN                |





$$\text{precision} = \frac{\text{TP}}{|\text{predicted as positive}|} = \frac{\text{TP}}{\text{TP} + \text{FP}}$$

$$\text{recall} = \text{sensitivity} = \text{true positive rate} = \text{probability of detection} = \frac{\text{TP}}{|\text{real positive}|} = \frac{\text{TP}}{\text{TP} + \text{FN}}$$

$$\text{specificity} = \text{true negative rate} = \frac{\text{TN}}{|\text{real negative}|} = \frac{\text{TN}}{\text{TN} + \text{FP}}$$

$$\text{accuracy} = \frac{|\text{correct prediction}|}{|\text{all samples}|} = \frac{\text{TP} + \text{TN}}{\text{TP} + \text{TN} + \text{FP} + \text{FN}}$$

$$\text{F1 score} = \frac{2 \times \text{precision} \times \text{recall}}{\text{precision} + \text{recall}}$$



**Accuracy** can be a misleading metric for imbalanced data sets because it can be biased by the most common target class. 

A high **sensitivity** test is reliable when its result is negative since it rarely misdiagnoses the cases which are indeed positive, it is not that reliable when its result is positive. 

A high **specificity** test is reliable when its result is positive since it rarely gives positive results in negative cases, it is not that reliable when its result is negative. A test with a higher specificity has a lower type I error rate.

The **ROC curve** is created by plotting the true positive rate (TPR) against the false positive rate (FPR) at various threshold settings. **True positive rate (TPR)** is also known as recall, sensitivity or probability of detection. **false positive rate (FPR)** can be calculated as $1 - \text{specificity}$. 

![roc_curve](/assets/images/blog/roc_curve.png)



| English   | Chinese        |
|-----------|----------------|
| precision | 精确率，查准率 |
| recall    | 召回率，查全率 |
| sensitivity    | 灵敏度 |
| specificity    | 特异度 |
| accuracy    | 准确率 |
| confusion matrix    | 混淆矩阵 |













