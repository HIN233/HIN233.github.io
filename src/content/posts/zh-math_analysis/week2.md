---
title: 数学分析习题3
date: 2024-12-27
summary: 数学分析函数习题（三），主要训练计算、证明的能力
category: 习题
tags: [数学分析, 习题, 函数]
---

## 本周简介

单变量微分学的知识到 $Taylor$ 定理就大致结束了,本周对导数、中值定理和 $Taylor$ 定理做一些复习.
线下会挑一部分题出来讲解.

史济怀先生的数学分析教程中有这样一段话:

> “我们不想把话说得太绝对，但至少可以说:凡是用一元微分学中的定理、技巧能解决的问题,其中的大部分都可以用 Taylor 定理来解决. 掌握了 Taylor 定理之后，回过头去看前面的那些理论,似乎一切都在你的掌握之中,使你有一种'会当凌绝顶,一览众山小’的意境.从这个意义上说'Taylor 定理是一元微分学的顶峰’,并不过分。”

## 习题

1. 设 $f$ 在 $(−\infty,+\infty)$ 上二阶可微, 且有界,证明: 存在$\xi$,使成立 $f^{\prime\prime}(\xi)=0$ .
2. 设 $f$ 在 $(−\infty,+\infty)$ 上可导,且，满足 $af(x)+bf(\frac{1}{x})=\frac{c}{x}$ ,其中 $a,b,c$ 均为常数, $\lvert a \rvert\neq \lvert b \rvert$ , 求 $f^{\prime}(x)$ .
3. 设 $f$ 在 $[0,2]$ 上二阶可微, 且 $|f(x)|\leq1$ , $|f^{\prime\prime}(x)| \leq 1$ , 证明: $|f^\prime(x)| \leq 2$.
4. 求曲线
   $$
   \begin{cases}
   x = t^3+4t ,\\
   y = 6t^2 ,
   \end{cases}
   $$
   上的的点满足:该点处的切线与直线
   $$
   \begin{cases}
   x = -7t ,\\
   y = 12t-5 ,
   \end{cases}
   $$
   平行.
5. 设 $f$ 在 $[a,b]$ 上可导,且 $f^\prime_+(a) · f^\prime _-(b)<0$ ,证明:在 $(a,b)$ 内至少存在一点 $\xi$ ,使得 $f^\prime(\xi)=0$.
6. 证明近似公式 $\sqrt[n]{a^n+b}\approx a+\frac{b}{na^{n-1}} \quad (\lvert b \rvert \ll a^n)$ .
7. 计算 $\frac{\arcsin x}{\sqrt{1-x^2}}$ 的带 $Peano$ 余项的 $Maclaurin$ 公式.
8. 求极限
   $$
   \lim \limits_{x\rightarrow 0} \frac{e^{-\frac{x^2}{2}}-\cos x}{x^2[3x+\ln (1-3x)]}.
   $$
9. 设 $f$ 在 $x=0$ 的邻域内二阶可导,且 $\lim \limits_{x\rightarrow 0} \frac{\sin 3x +xf(x)}{x^3} = 0$ ,求 $f(0),f^\prime(0),f^{\prime\prime}(0)$ .

10. 设 $f(x)$ 在 $[0,1]$ 上连续, $f(x)$ 在 $(0,1)$ 内可导,且 $f(0)=0$ , $f(1)=1$ . 证明:
    (1)存在 $x_0 \in (0,1)$ 使得 $f(x_0)=2-3x_0$ ;
    (2)存在$\xi ,\eta \in (0,1)$, 且 $\xi \neq \eta$ ,使得 $[1+f^\prime(\xi)][1+f^\prime(\eta)]= 4$ .

11. 设 $x_0 \in (0,\frac{\pi}{2})$ , $x_n = \sin x_{n-1}$ , $n \in \mathbb{N}_+$ ,证明: $x_n \sim \sqrt{\frac{3}{n}} (n \rightarrow \infty)$.

## Hint

**第七题** 利用递推公式
**第八题** 利用带 $Peano$ 余项的 $Taylor$ 展开
**第十题** (第十二届CMC非数竞赛预赛第三题)第一题利用零点存在定理,第二题利用第一小问得到的 $x_0$ ,在 $[0,x_0]$ 和 $[x_0,1]$ 中分别运用 $Lagrange$ 中值定理
**第十一题** 运用 $stolz$ 定理
