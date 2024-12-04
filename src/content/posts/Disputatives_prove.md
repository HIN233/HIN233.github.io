---
title: 好友投稿：一个有趣的证明
date: 2024-12-04
summary: 对于一维迭代动力系统中一个定理的证明
category: 数学分析
tags: [数学分析, 动力系统, 证明]
---

# 命题

设函数$f: [a,b] \rightarrow [a,b] $ 且 $f \in C([a,b])$ . 若 $f$ 没有 $2-$周期点，则任意点 $x \in [a,b]$ 的轨道 $\{f^n(x)\}$ 均收敛.

# 证明

先证明**任意点 $x \in [a,b]$ 的轨道 $\{f^n(x)\}$ 的子列收敛于不动点**. <br>
因为 $\{f^n(x)\} \subset [a,b]$ ，根据$Bolzano-Weierstrass$定理， $\{f^n(x)\}$ 存在收敛的子列.<br>
_那么这个子列收敛于哪个点呢？直觉上收敛于不动点，下证_<br>
假设这个子列收敛于 $\xi$ ，当

$$
f^{n_k}(x) = x_{n_{k+1}} \rightarrow \xi
$$

时，有

$$
f(x_{n_{k+1}})=x_{n_{k+1}+1} \rightarrow f(\xi)
$$

，继而

$$
f(x_{n_{k+1}+1})=x_{n_{k+1}+2} \rightarrow f(f(\xi))
$$

$$
\dots
$$

$$
f(x_{n_{k+1}+i})=x_{n_{k+1}+i+1} \rightarrow f^{i+1}(\xi))
$$

如此不断地做下去可以得到

$$
f(x_{n_{k+2}-1})=x_{n_{k+2}} \rightarrow f^{j}(\xi) \qquad (j=n_{k+2}-n_{k+1})
$$

因为由 $x_{n_{k+1}} \rightarrow \xi$ 得到了 $x_{n_{k+2}} \rightarrow f^{j}(\xi)$ ，所以 $f^{j}(\xi) = \xi$ , 这表示 $\xi$ 是周期点.
事实上，$\xi$ 不可能是周期大于一的周期点，题目里已经限制了不存在$2-$周期点，当周期大于等于三的时候，根据 $Sharkovsky$ 定理的周期推导序列以及 $Li-Yorke$ 的结果，若如果有三周期点，则有所有周期点，若周期数是偶数，可以推出序列中有$2-$周期点，所以也是不可能的. 那么情况只剩下了周期是一的不动点.
如果 $\xi$ 不是不动点，那么

$$
f^{j}(\xi) \neq \xi ,\quad \forall j \in \mathbb{N}
$$

，这个子列也就不收敛了，矛盾. <par>
至此，我们证明了所有极限点都是不动点，也就是证明了这个函数在 $[a,b]$ 内存在不动点，而任意点的轨道的极限点是某个不动点.

\*接下来的步骤和上面很像，核心思路是：**通过这个子列收敛得到整个轨道收敛\***

为了方便，重新定义这个子列下标得子列 $x_{m_k}$ . 由$f$的连续性，又

$$
x_{m_k} \rightarrow \xi
$$

得到

$$
x_{m_k+1}=f(x_{m_k}) \rightarrow f(\xi)=\xi
$$

，继而

$$
x_{m_k+2}=f(x_{m_k+1}) \rightarrow \xi
$$

$$
\dots
$$

$$
x_{m_k+i} \rightarrow \xi
$$

$$
\dots
$$

如此往复，直到得到

$$
x_{m_{k+i}} \rightarrow \xi ,\quad \forall i \in \mathbb{N}
$$

利用这个循环，得到??从任意点出发的轨道整体是收敛的.

# 特别鸣谢

提供命题的好朋友：

做出解答的好朋友：[Disputative](/friends)

以及提供帮助的数学分析老师.
