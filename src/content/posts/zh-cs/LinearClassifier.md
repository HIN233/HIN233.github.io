---
title: Linear Classifier
date: 2025-03-20
summary: 线性分类器的三种视角以及损失函数的推导
category: 深度学习
tags: [深度学习, 损失函数, 线性分类器]
---

## Three ways to think about Linear Classifier

- Algebraic Viewpoint: f(x,W) = Wx
- Visual Viewpoint: One template (which may be strange due to a single template cannot capture multiple modes of the data) per class
- Geometric Viewpoint: Hyperplanes cutting up space

## Loss Functions quantify preferences

<div style="text-align: center;">
<img src="https://s2.loli.net/2025/03/08/CfOXMkKRdDxU9gE.png" alt="Linear Classifier" width="50%" />
</div>

### Score function

$s = f(x;W,b) = Wx+b$

### Loss function

1. Softmax Cross Entropy Loss
   $$L_i = -\log(\frac{e^{s_{y_i}}}{\sum_j e^{s_j}})$$

2. Multi-Class SVM Loss ("Hinge Loss")
   $$L_i = \sum_{j\neq y_i} \max(0, s_j - s_{y_i} + \Delta),$$
   where $\Delta$ is the margin, which is a hyperparameter and we set it to 1 in practice.

### Direvetive

#### Softmax Cross Entropy Loss from [here](https://zhuanlan.zhihu.com/p/131647655)

$$\frac{\partial L_i}{\partial s_{j}} = \begin{cases} S(s_j) - 1 & \text{if } j = y_i \\ S(s_j) & \text{if } j \neq y_i \end{cases}$$

### Full loss & Regularization

$$L = \frac{1}{N} \sum_i L_i + \lambda R(W)$$
where $R(W)$ is the regularization term, and $\lambda$ (The tradeoff between minimizing cost function and avoiding overfitting) is a hyperparameter.

### Tip on Debugging

Check the loss at chance (e.g. randomly initialized weights should give loss of $-\log(0.1)$ for 10 classes, since chance is 0.1 for each class).
