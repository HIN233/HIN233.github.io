---
title: 数学分析习题1
date: 2024-12-04
summary: 数学分析函数习题（一），主要训练举反例、计算、证明的能力
category: 习题
tags: [数学分析, 习题, 函数]
---

## 前言（策划）

目前（12/04暂定）的数学分析方面的活动主要有

- 不定期（每周至少有）产出习题一份
- 每次线下有若干个*值得注意的*知识点分享+同学投稿和讲解（+某些题目讲解，可能有），固定答疑
- 线上答疑群，另外我会慢慢把资料整理出来（会有个地方挂着下载链接）

## 序（一）

每周不定期更新习题，主要是训练思维、强化手感为主，难以囊括到所有的知识，更重要的是需要自己看书梳理知识网络。
Features:

- 部分附有Hint
- 解析: 大部分有
- 类型: 绝大部分为举反例，计算和证明题
- 题源: 绝大部分给出
- 难度: 不等，中等多，偏下第二，偏上第三

## 本周简介

本次主要以函数的极限为主，以及少量的连续函数知识，考虑到学期末还有部分实数基本定理的内容，数列后面再更新。主要题源：

- 《数学分析习题课讲义（第2版）》上册(谢惠民)
- 《数学分析中的问题和反例》(汪林)

## 习题

### 判断

1. 若函数 $f$ 在的 $x_0$ 任何邻域内都是无界的,那么当 $x\rightarrow x_0$ 时, $f$ 是无穷大量.
2. 只要函数 $f$ 和 $g$ 在 $x=x_0$ 处有一个或一个以上不连续，那么 $fg$ ($f$和$g$的乘积)在 $x=x_0$ 处不连续.
3. 若函数 $y=f(u)$ 和 $u=g(u)$ ,其复合函数 $f[g(x)]$ 处处连续，并适合$\lim_{u\rightarrow b}f(u)=c, \lim_{x\rightarrow a}g(x)=b,$
   那么$\lim_{x\rightarrow a}f[g(x)]=c$.
4. 若 $f$ 分别在 $I_1$ 和 $I_2$ 上一致连续,则 $f$ 在 $I=I_1 \cup I_2$ 上也一致连续.
5. 若$\forall \epsilon >0,\exists n,\forall x \in U^{\degree}(a;\frac{1}{n}),$成立$\lvert f(x)-A \rvert < \epsilon$,则$\lim \limits_{x\rightarrow a}=A$.
6. 若$\forall n\in \mathbb{N}_+,\exists \delta >0,\forall x \in U^{\degree}(a;\delta),$成立$\lvert f(x)-A \rvert < \frac{1}{n}$,则$\lim \limits_{x\rightarrow a}=A$.
7. 若$\exists \delta >0,\forall \epsilon > 0,\forall x \in U^{\degree}(a;\delta),$成立$\lvert f(x)-A \rvert < \epsilon$,则$\lim \limits_{x\rightarrow a}=A$.
8. 若$\forall \delta >0,\exists \epsilon > 0,\forall x \in U^{\degree}(a;\delta),$成立$\lvert f(x)-A \rvert < \epsilon$,则$\lim \limits_{x\rightarrow a}=A$.

### 计算

9. $\lim \limits_{x\rightarrow \infty}(\frac{2}{\pi}\arctan x)^x$.
10. $\lim \limits_{x\rightarrow 1}(1-x)\tan (\frac{\pi}{2}x)$.
11. 设 $a_1,a_2,\dots ,a_n$ 为正数, $n\geq 2$ , $f(x)=(\frac{a_1^x+a_2^x+\dots +a_n^x}{n})^{\frac{1}{x}}$ ,求 $\lim \limits_{x\rightarrow 0}f(x)$.

    用等价量代换方法计算下列极限:

12. $\lim \limits_{x \rightarrow 0}\frac{\ln (\sin^2 x+e^x)-x}{\ln (x^2+e^{2x})-2x}$.
13. $\lim \limits_{x \rightarrow 0}\frac{\sqrt{(\cos x)}-\sqrt[3]{(\cos x)}}{\sin ^2x}$.
14. $\lim \limits_{x \rightarrow 0}\frac{(3+2\sin x)^x-3^x}{\tan ^2 x}$.
15. $\lim \limits_{t \rightarrow 0}(\frac{\arcsin t}{t})^{\frac{1}{t^2}}$.
16. 设 $a>0,a\neq 1$,求 $\lim \limits_{x \rightarrow \infty}(\frac{1}{x} \frac{a^x-1}{a-1})^{\frac{1}{x}}$.

### 证明

17. 对多项式 $p_n(x)=a_0x^n+a_1x^{n-1}+\dots +a_n$ 证明: $\lim \limits_{x\rightarrow a}p_n(x) = p_n(a)$.
18. 已知 $\lim \limits_{n\rightarrow \infty}a_n=a$ , 证明: $\lim \limits_{n\rightarrow \infty}e^{a_n}=e^{a}$.
19. 证明: 在区间 $(a,+\infty)$ 上单调有界函数 $f$ 一定存在极限 $\lim \limits_{x\rightarrow \infty}f(x)$.
20. 证明: $\ln x = o(x^{-\alpha})(x\rightarrow 0^+)\quad(\alpha >0)$.
21. 证明: $O(x^2)=o(x)(x\rightarrow 0)$.

### 题源 & Hint

1. (T2汪林p74) 无界函数的定义与函数趋于无穷大的定义有些相似. 然而,这两个概念有本质上的差别. 无穷大的条件比无界更强.
2. (T14汪林p78) 若函数 $f$ 和 $g$ 与在 $x=x_0$ 处皆连续,则$fg$在$x=x_0$处亦连续;但是二者在 $x=x_0$ 处不同时连续时，$fg$ 在 $x=x_0$ 的连续性未知. 可以想想各种情况的例子.
3. (T17汪林p82) 复合函数的连续性定理具有很重要的意义,使用时常常要注意自变量的代换是有一定条件的.从极限的角度看就是内层函数趋于极限的时候不能取到这样的值,使得外层函数在以这个值为自变量的时候无定义.如果从连续的角度看,可以让外层函数在该点连续.参考谢惠民p101.
4. (T37汪林p94) 此定理需要区间$I_1$的右端点属于$I_1$且区间$I_2$的左端点属于$I_2$(例12华东师大数分p77)
5. (4.1.3思考题T1(4)谢惠民)
6. (4.1.3思考题T1(3)谢惠民)
7. (4.1.3思考题T2(1)谢惠民) 条件过强,需要在某邻域内 $f(x)\equiv A$
8. (4.1.3思考题T2(2)谢惠民) 条件过弱,只需 $\epsilon$ 充分大即可
9. (4.3.4练习题谢惠民T1(1)) $e^{-2/\pi}$
10. (4.3.4练习题谢惠民T1(1)) $2/\pi$
11. (4.3.4练习题谢惠民T4) $\sqrt[n]{a_1a_2\dots a_n}$
12. (4.4.4练习题谢惠民T4(1)) $1$
13. (4.4.4练习题谢惠民T4(4)) $-1/12$
14. (4.4.4练习题谢惠民T4(5)) $2/3$
15. (4.4.4练习题谢惠民T4(6)) $e^{\frac{1}{6}}$
16. (4.5.2参考题谢惠民T5) 注意分类讨论
17. (思考题 谢惠民p99)
18. 利用连续函数的性质与归结原则
19. (4.2.5练习题谢惠民T7) 利用单调有界定理证明 $\{f(n)\}$有极限,再利用夹逼准则
20. (习题课)
21. (例4.4.1谢惠民) 利用定义

## 后续计划

更新连续函数，导数，再是实数定理和数列极限
