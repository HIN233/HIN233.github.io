---
title: Optimization
date: 2025-03-20
summary: 优化算法的介绍
category: 深度学习
tags: [深度学习, 优化算法, 梯度下降法]
---

## Computing Gradients

- Numeric gradient: approximate, slow, easy to write
- Analytic gradient: exact, fast, error-prone

In practice: Always use analytic gradient, but check implementation with numerical gradient. This is called a **gradient check**.

> **torch.autograd.gradcheck**(_func, inputs, eps=1e-06, atol=1e-05, rtol=0.001, raise_exception=True, check_sparse_nnz=False, nondet_to1=0.0_)
>
> Check gradients computed via small finite differences against analytical gradients w.r.t. tensors in inputs that are of floating point type and with requires_grad=True.
>
> The check between numerical and analytical gradients uses allclose() .

> **torch.autograd.gradgradcheck**(_func, inputs, grad_outputs=None, eps=1e-06, atol=1e- 95, rtol=0.001, gen_non_contig_grad_outputs=False, raise_exception=True, nondet_tol=0.0_)
>
> Check gradients of gradients computed via small finite differences against analytical gradients w.r.t. tensors in `inputs` and `grad_outputs` that are of floating point type and with `requires_grad=True`.
>
> This function checks that backpropagating through the gradients computed to the given grad_outputs are correct.

## Algorithm of Gradients Descent

![optimization.png](https://s2.loli.net/2025/03/09/syMHt3J8fEW4LgQ.png 'Overview')

### Vanilla Gradient Descent (GD)

Iteratively step in the direction of the negative gradient (direction of local steepest descent)

```python
w = initial_weight()
for _ in range(n_steps):
    dw = compute_gradient(loss_function, data, w)
    w -= learning_rate * dw
```

Hyperparameters:

- Weight initialization method
- Learning rate
- Number of steps

### Stochastic Gradient Descent (SGD)

```python
w = initial_weight()
for _ in range(n_steps):
    minibatch = sample_data(data, batch_size)
    dw = compute_gradient(loss_function, minibatch, w)
    w -= learning_rate * dw
```

Hyperparameters:

- Weight initialization method
- Learning rate
- Number of steps
- Batch size
- Data sampling method

Approximate sum using a minibatch of examples 32 / 64 / 128 common

Problems:

- 当成本函数在某个方向上的梯度很大，在另一个方向上的梯度很小时，这会导致成本函数会出现来回大幅度波折的情况，收敛缓慢，消耗大量时间和计算资源.
- Stop at _local minimum_ or **saddle point**
- 可能有很大的噪声干扰

### SGD + Momentum

Combine gradient at current point with velocity to get step used to update weights

$$v_{t+1} = \rho v_t + \nabla f(x_t)$$
$$x_{t+1} = x_t - \alpha v_{t+1}$$

```python
v = 0
for _ in range(n_steps):
    dw = compute_gradient(w)
    v = rho * v + dw
    w -= learning_rate * v
```

Rho gives “friction”; typically rho=0.9 or 0.99

Different way (but they are equivalent - give same sequence of x):

$$v_{t+1} = \rho v_t - \alpha f(x_t)$$
$$x_{t+1} = x_t + v_{t+1}$$

```python
v = 0
for _ in range(n_steps):
    dw = compute_gradient(w)
    v = rho * v - learning_rate * dw
    w += v
```

### Nestrov Accelerated Gradient (NAG)

“Look ahead” to the point where updating using velocity would take us; compute gradient there and mix it with velocity to get actual update direction

$$v_{t+1} = \rho v_t - \alpha \nabla f(x_t + \rho v_t)$$
$$x_{t+1} = x_t + v_{t+1}$$
$\Rightarrow (\widetilde{x}_t = x_t + \rho v_t) \Rightarrow $
$$v_{t+1} = \rho v_t - \alpha \nabla f(\widetilde{x}_t)$$
$$\widetilde{x}_{t+1} - \rho v_{t+1} = \widetilde{x}_t - \rho v_t +v_{t+1} $$
$$\rightarrow \widetilde{x}_{t+1} = \widetilde{x}_t + v_{t+1} + \rho (\widetilde{x}_{t+1} - \widetilde{x}_t) \quad \star$$
$$or = \widetilde{x}_t + \rho^2 v_t - (1+\rho)\alpha \nabla f(\widetilde{x}_t)$$

```python
v = 0
for _ in range(n_steps):
    dw = compute_gradient(w - rho * v)
    old_v = v
    v = rho * v - learning_rate * dw
    w -=  rho * old_v - (1 + rho) * v
```

$$v_{t+1} = \rho v_t - \nabla f(x_t + \rho v_t)$$
$$x_{t+1} = x_t + \alpha v_{t+1}$$
$$or = \alpha \rho v_t - \alpha \nabla f(x_t)$$
$\Rightarrow (\widetilde{x}_t = x_t + \rho v_t) \Rightarrow $
$$v_{t+1} = \rho v_t - \nabla f(\widetilde{x}_t)$$
$$\widetilde{x}_{t+1} = \widetilde{x}_t + \alpha v_{t+1} + \rho (\widetilde{x}_{t+1} - \widetilde{x}_t) \quad \star$$
$$or = \widetilde{x}_t + (\alpha \rho - \rho + \rho^2) v_t - (\alpha+\rho)\nabla f(\widetilde{x}_t)$$

In my opinion, the difference between Momentum and NAG is that NAG **drops the volume of the velocity at current point**, and **turns up the volume of gradient**, which is the reason of NAG "looks ahead" from the perspective of discrete data.

### AdaGrad

Added element-wise scaling of the gradient based on the historical sum of squares in each dimension
“Per-parameter learning rates” or “**adaptive learning rates**”

```python
cache = 0
for _ in range(n_steps):
    dw = compute_gradient(w)
    cache += dw**2
    w -= learning_rate * dw / (sqrt(cache) + epsilon)
```

### RMSProp: “Leaky Adagrad”

```python
cache = 0
for _ in range(n_steps):
    dw = compute_gradient(w)
    cache = decay_rate * cache + (1 - decay_rate) * dw**2
    w -= learning_rate * dw / (sqrt(cache) + epsilon)
```

### Adam: RMSProp + Momentum

```python
moment1 = 0
moment2 = 0
for t in range(1, n_steps + 1):
    dw = compute_gradient(w)
    moment1 = beta1 * moment1 + (1 - beta1) * dw    # Momentum
    moment2 = beta2 * moment2 + (1 - beta2) * dw**2 .   # RMSProp
    moment1_unbias = moment1 / (1 - beta1**t)   # Bias correction1
    moment2_unbias = moment2 / (1 - beta2**t)   # Bias correction2
    w -= learning_rate * moment1 / (sqrt(v) + epsilon)
```

**Note**: Bias correction for the fact that first and second moment estimates start at zero

Adam with beta1 = 0.9,beta2 = 0.999, and learning_rate = 1e-3, 5e-4, 1e-4 is a great starting point for many models!

### L2 Regularization vs Weight Decay

L2 regularization:
$$\mathcal{L} = \mathcal{L}_{\text{data}} + \lambda |w|^2$$
$$g_t = \nabla \mathcal{L}(w_t) = \nabla \mathcal{L}_{data} + 2\lambda w_t$$
$$s_t = optimizer(g_t)$$
$$ w\_{t+1} = w_t - \alpha s_t$$

Weight decay:
$$\mathcal{L} = \mathcal{L}_{\text{data}}$$
$$g_t = \nabla \mathcal{L}_{data}(w_t)$$
$$s_t = optimizer(g_t)+ 2\lambda w_t$$
$$ w\_{t+1} = w_t - \alpha s_t$$

L2 Regularization and Weight Decay are **equivalent** for **SGD, SGD+Momentum** so people often use the terms interchangeably!
But they are not the same for **adaptive methods** (AdaGrad, RMSProp, Adam, etc)

### AdamW: Decoupled Weight Decay

![AdamW.png](https://s2.loli.net/2025/03/09/Yk9fZhgAMUdc3xj.png)

AdamW should probably be your “default” optimizer for new problems

### Second-Order Optimization

1. Use gradient and Hessian to make quadratic approximation
2. Step to minimize the approximation

- Quasi-Newton methods (BGFS most popular): instead of inverting the Hessian (O(n^3)), approximate inverse Hessian with rank 1 updates over time (O(n^2) each).
- L-BFGS (Limited memory BFGS): Does not form/store the full inverse Hessian.
- Usually works very well in full batch, deterministic mode
- Does not transfer very well to mini-batch setting. Adapting second-order methods to large-scale, stochastic setting is an active area of research.

## In practice

- **Adam** is a good default choice in many cases
  **SGD+Momentum** can outperform Adam but may require more tuning
- If you can afford to do full batch updates then try out L-BFGS (and don’t forget to disable all sources of noise)
