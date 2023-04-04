---
layout: post
title:
tags: [Signals-and-Systems]
permalink: /2023-spring/signals-and-systems/convolution-in-ct
---

# Convolution in C.T.

## Recall: Convolution in D.T.

For LTI system, $$h[n]$$ denote the impulse response to the signal $$\delta[n]$$. Thanks to superposition, general input signal $$x[n]$$ can be written as

$$
x[n]=\sum_{k=-\infty}^\infty x[k]\delta[n-k]
$$

It can be easily observed that $$x[k]\delta[n-k]= x[n]$$ if $$k=n$$.

Also, the output of signal is given by the convolution sum

$$
y[n] = \sum_{k=-\infty}^\infty x[k]h[n-k]
$$

# Convolution in Continous Time

## Sifting Property

The convolution sum for discrete system is based on the **sifting principle**, that is, the input signal can be represented as a superposition of scaled and shifted impulse function. This property can be generalized to continuous signals, by thinking impulse function as arbitrary thin pulse.

### Signal Stair Case Approximation

Similar to the discrete time case, any continuous signal can be approximated by a linear combination(superposition) of thin pulse,

$$
\delta_\Delta=\begin{cases}
\frac{1}{\Delta} & 0\le t \le \Delta\\
0 &\text{otherwise}
\end{cases}
$$

![Thin, delayed pulse](../../../assets/img/src/2023-Spring/delayed_pulse.png)

Thin, delayed pulse

Since $$\Delta\delta_\Delta$$ has unit amplitude, we have

$$
x(t) =\sum_{k=-\infty}^{\infty}x(k\Delta)\delta_\Delta(t-k\Delta)\Delta
$$

For any value of $$t$$, only one pulse $$x(k\Delta)\delta_\Delta(t-k\Delta)$$ is non-zero. When $$\Delta\rightarrow 0$$, the summation approaches an integral,

$$
\begin{equation}x(t) =\int_{-\infty}^{\infty}x(\tau)\delta(t-\tau)d\tau\end{equation}
$$

We refer to $$(1)$$ as a **sifting property** of continous impulse.

### Alternative Derivation

There is another derivation of sifting property of continuous impulse. The continuous unit impulse function has following properties,

$$
\begin{equation}
\delta(t-\tau) = 0 \;\;(t\neq \tau)
\end{equation}
$$

$$

\begin{equation}
\int_{-\infty}^{\infty}\delta(t-\tau) = 1
\end{equation}
$$

From $$(2)$$, we have $$x(\tau)\delta(t-\tau)=0$$ for $$t  \neq \tau$$.
Therefore, from $$(3)$$, we have

$$
\begin{align*}
\int_{-\infty}^{\infty}x(\tau)\delta(t-\tau)d\tau  &= \int_{-\infty}^{\infty} x(t)\delta(t-\tau)d\tau\\
&= x(t)\int_{-\infty}^{\infty}\delta(t-\tau)d\tau\cdots\text{from  } (3)\\
&= x(t)
\end{align*}
$$

This derivation emphasises the relationship between the structure for both discrete and continuous time signals. (They have similar structure)

## Examples

### Example 1

Consider a LTI system of input signal $$x(t)$$ and the impulse response $$h(t)$$

$$
x(t)=e^{-at}u(t) \;\;\;(a>0)\\
h(t)=u(t)
$$

Then, we have the convolution integral

$$
\begin{align*}
y(t)&=\int_{-\infty}^{\infty}x(\tau)h(t-\tau)d\tau\\
&=\int_0^{\infty}e^{-at}h(t-\tau)d\tau\end{align*}
$$

For $$t <0$$, $$h(t-\tau) = 0$$, therefore, we have $$y(t)=0$$ ($$t<0)$$

If $$t\ge0$$, then $$h(t-\tau) =1$$ if $$\tau \le t$$. Therefore,

$$
y(t) = \int_0^\infty e^{-a\tau}h(t-\tau) = \int_0^t e^{-a\tau} = \frac{1}{a}\big(1-e^{-at}\big)
$$

By combining $$y(t)$$ for both $$t \ge 0$$ and $$t<0$$, we have

$$
y(t)=\frac{1}{a}(1-e^{-at})u(t)
$$

### Example 2

Compute the convolution of following signals

$$
x(t) = e^{2t}u(-t)\\
h(t)=u(t-3)
$$

The convolution integral of $$x(t)$$ and $$y(t)$$ becomes

$$
\begin{align*}
y(t) &= \int_{-\infty}^{\infty}x(\tau)h(t-\tau)d\tau\\
&= \int_{-\infty}^{0}e^{2\tau}h(t-\tau)d\tau\\
\end{align*}
$$

For $$t\ge 3$$, $$t-\tau\ge 3$$ ($$\because -\infty < \tau \le 0)$$, therefore

$$
y(t) = \int_{-\infty}^{0}e^{2\tau}d\tau = \frac{1}{2}e^{2\tau}\bigg\|_{-\infty}^{0} = \frac{1}{2}
$$

For $$t < 3$$, $$h(t-\tau) =1$$ only if $$\tau \le t-3$$. Therefore,

$$
y(t) = \int_{-\infty}^{t-3} e^{2\tau}d\tau = \frac{1}{2}e^{2\tau}\bigg\|^{t-3}_\infty = \frac{1}{2}e^{2t-6}
$$

Therefore, the convolution of the signals $$x(t)$$ and $$h(t)$$ is

$$
y(t) = \begin{cases}\frac{1}{2} &t \ge 3\\
\frac{1}{2}e^{2t-6} & t<3 \end{cases}
$$

# Properties of LTI Systems

Any LTI system is completely described by its impulse response,

$$
y[n] = \sum_{k=-\infty}^{\infty}x[k]h[n-k]\\
y(t) = \int_{-\infty}^{\infty}x(\tau)h(t-\tau)d\tau
$$

For example, suppose a discrete time impulse response

$$
h[n] = \begin{cases}1 &n=0,1\\ 0 &\text{otherwise}\end{cases}
$$

Then, by computing convolution sum, we have

$$
y[n] = \cdots+x[n-1]h[1]+x[n]h[0] = x[n]+x[n-1]
$$

Thus, this impulse response completely discribes the LTI system above. However, there are many nonlinear systems with the same response,

$$
y[n]=(x[n]+x[n-1])^2\\
y[n]=\max(x[n], x[n-1])
$$

Therefore, nonlinear system is not completely characterized by impulse response.

## Commutative Property

Convolution is a commutative operator both in D.T. and C.T., that is,

$$
x[n]*h[n]=h[n]*x[ n]=\sum_{k=-\infty}^{\infty}h[k]x[n-k]\\
x(t)*h(t)=h(t)*x(t)=\int_{-\infty}^{\infty}h(t)x(t-\tau)d\tau
$$

Therefore, we can choose both of them in calculating, whichever appears the most straight forward.

## Distributive Property

Convolution is distributive, that is,

$$
x[n]*(h_1[n]+h_2[n]) = x[n]*h_1[n]+x[n]*h_2[n]\\
x(t)*(h_1(t)+h_2(t))=x(t)*h_1(t)+ x(t)*h_2(t)
$$

By distributive property, a parallel combination of LTI systems can be replaced by a single LTI system.

## Associative Property

Also, convolution of LTI system is associative,

$$
x[n]*(h_1[n]*h_2[n]) = (x[n]*h_1[n])*h_2[n]\\
x(t)*(h_1(t)*h_2(t) = (x(t)*h_1(t))*h_2(t)
$$

Therefore, a serial combination of LTI systems can be replaced by a single LTI system, or change its order.
