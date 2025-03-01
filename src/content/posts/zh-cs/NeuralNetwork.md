---
title: Neural Networks
date: 2025-03-01
summary: 神经网络，梯度下降法步骤以及反向传播算法的介绍
category: 深度学习
tags: [深度学习, 神经网络, 梯度下降法, 反向传播算法]
---

# Neural Networks

## Intro

人工神经网络主要考虑以下三个方面：

- 神经元的激活规则
- 网络的拓扑结构
- 学习算法

组成单元->感知机：能够容易地实现逻辑与、或、非运算

三个步骤

1. 定义网络
2. 损失函数 回归问题/分类问题
3. 优化(利用偏导数-利用微小扰动观察值的变化情况)

## 梯度下降法

1. Take the derivative of the Loss Function for each parameter in it.In fancy Machine Learning Lingo, take the Gradient of the Loss Function.
2. Pick random values for the parameters.
3. Plug the parameter values into the derivatives (the Gradient).
4. Calculate the Step Sizes: **Step Size = Slope x Learning Rate**.
5. Calculate the New Parameters by adding the **Step Size**.
6. Go back to **Step 3** and repeat untilStep Size is very small, or you reach the Maximum Number of Steps.

## Back Propagation

核心思想：将输出误差以某种形式通过隐层向输入层逐层反传

形式：多元复合函数求偏导的过程
