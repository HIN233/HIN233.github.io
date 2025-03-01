---
title: 数学分析习题2
date: 2024-12-04
summary: 数学分析函数习题（二），主要训练举反例、计算、证明的能力
category: 习题
tags: [数学分析, 习题, 函数]
---

## 本周简介

本次主要以连续函数(1.4.5.6.7.9.10.19.20.21.)和导数(2.3.11.13.14.15.17.)为主，以及少量的极限(8.12.16.)知识复习。主要题源：

- 《数学分析习题课讲义（第2版）》上册(谢惠民)
- ?

## 习题

### 判断

1. $f$ 在 $(a,b)$ 上的每一个子闭区间连续,则$f$ 在 $(a,b)$ 上连续.
2. $f$ 在 $x=0$ 可导,且 $f(0)=0$,则 $f^\prime (0)=0$ ;反之也成立.
3. 若$f$ 在 $x=x_0$ 可导,且 $f$ 是 $(-1,1)$ 上的奇函数,则$f^\prime (0)=0$.
4. 如果一个函数$f(x)$在区间$I$上有介值性,那么$f(x)$在区间$I$上有连续性.<br>定义介质性:若$f(x)$在区间$I$上有定义,且对于区间$I$上的任意两点$a<b$来说,任何一个$y\in [f(a),f(b)]$,都能找到$x\in [a,b]$且满足$y=f(x)$,那么就说$f(x)$在区间$I$上有介值性.
5. 定义在有界区间上的一致连续函数一定有界.

### 思考

6. 设函数$f,g$在$x=a$都不连续,问$f+g$,$fg$在$x=a$是否连续?
7. 区间上不是处处连续的函数,其值域可以是一个区间吗?

### 计算

8. 求 $a$ ,使当 $x\rightarrow 1$ 时, $1-x$ 与 $a(1-\sqrt[m]{x})(m\in \mathbb{N}_+)$ 为等价无穷小.

9. 求下列各题中常数 $a$ , $b$ 的值,使函数 $f(x)$ 为连续函数
   $$
   (1)\quad
   f(x)=\left\{
   \begin{aligned}
   \frac{\sin ax}{x}, & & {x<0,} \\
   1, & & {x=0,} \\
   \frac{b(\sqrt{1+x}-1)}{x}, & & {x>0;} \\
   \end{aligned}
   \right.
   $$

$$
(2)\quad
f(x)=\lim \limits_{n \rightarrow \infty} \frac{x^{2n-1}+ax^2+bx}{x^{2n}+1}.
$$

10. 设

    $$
    f(x)=\left\{
    \begin{aligned}
    x^a\sin \frac{1}{x}, & & {x>0,} \\
    e^x+b, & & {x\leq 0,} \\
    \end{aligned}
    \right.
    $$

    试根据 $a$ 与 $b$ 的不同取值,讨论 $f(x)$ 在 $x=0$ 处的连续性(连续,左连续,右连续或间断性,在间断时指出其所属类型).

11. 设 $y=\frac{e^x+\sin x}{\sqrt{x}}$ ,求 $dy$.
12. 计算下列极限:

    $$
    (1)\lim \limits _{x\rightarrow 0} \frac{1-\cos x}{(e^x-1)ln(1+x)},
    $$

    $$
    (2)\lim \limits _{x\rightarrow \pi} \frac{\sin x}{\pi -x},
    $$

    $$
    (3)\lim \limits _{x\rightarrow 0} \frac{\sqrt{1+x+x^2}-1}{\sin 2x},
    $$

    $$
    (4)\lim \limits _{x\rightarrow 0} (\frac{2^x+3^x}{2})^{\frac{1}{x}}.
    $$

13. 笛卡尔叶形线的参数方程为

    $$
    \begin{cases}
    x = \dfrac{3a t}{1 + t^3} ,\\\\
    y = \dfrac{3a t^2}{1 + t^3} ,
    \end{cases}
    $$

    求 $y=y(x)$ 的导数.

14. 设 $a>0$ ,星形线的参数方程为

    $$
    \begin{cases}
    x = a \cos ^2t ,\\
    y = a \sin ^3t ,
    \end{cases}
    $$

    证明:星形线上任意处的切线被坐标轴所截线段长度为常数.

15. 求 $\frac{d}{dx} a^{x^x}$.(利用对数求导法)

16. 计算 $\lim \limits_{n\rightarrow \infty}[n\sin (2\pi \sqrt{n^2+1})]$ .

### 证明

17. 设 $\varphi (x),h(x)$ 在点 $x_0$ 的某邻域内有定义, $\varphi (x)$ 在点 $x_0$ 处可导,$h(x)$ 以在点 $x_0$ 处连续但不可导. 证明: $f(x)=\varphi (x)h(x)$ 在点 $x_0$ 处可导的充要条件为 $\varphi (x_0)=0$.

18. 设函数 $f(x) \in [0,1]$,且 $f(x)$ 只取有理值;若 $f(\frac{1}{3})=2$,证明:
    $$
    f(x)=2\quad \forall x\in [0,1]
    $$
19. (5.2.5例题谢惠民) 设函数 $f∈ C[a,b]$. 若 $\forall x \in [a,b], \exists y \in [a,b]$,使得 $|f(y)|\leq \frac{1}{2}|f(x)|$. 证明: $f$ 在 $[a,b]$ 中有零点.

20. (5.1.4练习题谢惠民T3) 设函数 $f∈ C[a,b]$. 若有数列 ${x_n}\in[a,b]$,使得 $\lim \limits _{n\rightarrow \infty}f(x_n)=A$ ,证明: 存在 $\xi \in[a,b]$,使得 $f(\xi)= A$.

21. (5.1.4练习题谢惠民T12)我们定义**函数在一个点的振幅**,即对于点 $a$ 的某邻域 $U(a;\delta)$ ,定义 $f$ 在这个邻域上的振幅为
    $$
    \omega _f(a,\delta) = \sup \limits _{x\in U(a;\delta)} \{f(x)\} - \inf \limits _{x\in U(a;\delta)}\{f(x)\} ,
    $$
    然后令
    $$
    \omega _f(a) = \lim \limits _{\delta \rightarrow 0^+} \omega _f(a,\delta),
    $$
    称 $\omega _f(a)$ 为 $f$ 在点 $a$ 的振幅. 证明: $f$ 在点 $a$ 处连续的充分必要条件为 $\omega _f(a)=0$.

## Hint & 题源
