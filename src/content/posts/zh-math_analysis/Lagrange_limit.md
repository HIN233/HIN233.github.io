---
title: 利用Language中值定理求极限
date: 2024-12-27
summary: 介绍了Lagrange中值定理的一种应用来求极限。
category: 数学分析
tags: [数学分析, Lagrange中值定理, 极限]
---

## 前言

Lagrange中值定理常见于证明题，而其优秀的性质还可以用于求极限。

## Recall

$$
设函数f(x)在[a,b]上连续,(a,b)上可导,则至少存在一点\xi \in (a,b),使得f^\prime(\xi)= \frac{f(a)-f(b)}{a-b}.
$$

## 例题

> (《大学生数学竞赛》蒲和平)求极限
>
> $$
> \lim \limits _{n\rightarrow \infty} n^2(\arctan \frac{a}{n} - \arctan \frac{a}{n+1}) \quad (a \neq 0)
> $$

**分析** 设 $f(x)=\arctan x$ ,利用 $Lagrange$ 中值定理将极限化简.
**解** 考虑 $Hiene$ 定理, 原极限等于

$$
\lim \limits_{x \rightarrow \infty} x^2(\arctan \frac{a}{x} - \arctan \frac{a}{x+1}).
$$

设 $f(x)=\arctan x$ , $f^\prime (x)= \frac{1}{1+x^2}$ ,根据 $Lagrange$ 中值定理,原极限等于

$$
L=\lim \limits_{x \rightarrow \infty} x^2[\frac{1}{1+\xi^2}(\frac{a}{x} -\frac{a}{x+1})], \qquad \xi \in (\frac{a}{x+1} , \frac{a}{x})
$$

令 $x\rightarrow \infty$ ,根据夹逼定理,

$$
0=\lim \limits_{x\rightarrow \infty} \frac{a}{x+1} \leq \lim \limits_{x\rightarrow \infty} \xi \leq \lim \limits_{x\rightarrow \infty} \frac{a}{x} = 0,
$$

$\Rightarrow \xi \rightarrow 0 \quad(x\rightarrow \infty).$
所以

$$
L = \lim \limits_{x \rightarrow \infty} x^2[\frac{1}{1+0^2}(\frac{a}{x} -\frac{a}{x+1})] = \lim \limits_{x \rightarrow \infty} \frac{ax^2}{x(x+1)} = a.
$$

**Remark**

1. 当遇到函数的增量时可以考虑 $Lagrange$ 中值定理
2. 解题步骤一般如下:
   - 找函数 $f(x)$
   - 使用 $Lagrange$ 中值定理化简原极限
   - 确定 $\xi$ 范围,利用夹逼定理,求出 $\xi$ 的值,代入极限化简
   - 求解极限

## 习题

求解下列极限

1. $\lim \limits_{x\rightarrow \infty} x^2(a^{\frac{1}{x}}-a^{\frac{1}{x+1}}) \quad (a>0),$
2. $\lim \limits_{x\rightarrow 0} \frac{\ln (\cos x)}{x^2},$
3. $\lim \limits_{x\rightarrow a}(\frac{\sin x}{\sin a})^{\frac{1}{x-a}} \quad (a \neq k\pi),$
4. $\lim \limits_{x\rightarrow 0}(\frac{\ln (1+x)}{x})^{\frac{1}{e^x-1}}.$

## Hint

1. 原极限等于 $\ln a$ ;构造$f(x) = a^x$ .
2. 原极限等于 $-\frac{1}{2}$ ;构造$f(x) = \ln x$ ,将分子看作 $\ln (\cos x)-\ln 0$ .
3. 原极限等于 $e^{\cot a}$ ;构造$f(x) = \ln x$ ;将原极限化成
   $$
   \lim \limits_{x\rightarrow a} \frac{1}{\sin a} \frac{\sin x - \sin a}{x-a}
   $$
   后既可以使用导数定义化为 $\cos a$ ,也可以继续使用 $Lagrange$ 中值定理, 构造$f(x) = \sin x$ .
4. 原极限等于 $e^{-\frac{1}{2}}$ ; 构造$f(x) = \ln x$ , $\xi$ 在 $\ln (1+x)$ 和 $x$ 之间,当 $x\rightarrow +\infty$ 时,可以认为 $\xi \sim x$ .
