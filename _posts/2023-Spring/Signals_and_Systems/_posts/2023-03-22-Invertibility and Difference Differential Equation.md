---
layout: post
title:
tags: [Signals-and-Systems]
permalink: /2023-spring/signals-and-systems/invertibility
---

# Invertibility and Difference/Differential Equations

# System Invertibility

## Definition

Suppose a serial system consists of system with a impulse response $$h(t)$$ and a system with impulse response $$h_1(t)$$, then it becomes $$y(t) = x(t)$$.

$$
x(t) \rightarrow \boxed{h(t)} \rightarrow \boxed{h_1(t)}\rightarrow y(t) = x(t)
$$

If $$y(t) = x(t)$$, then

$$
\begin{align*}
y(t) &= x(t)*h(t)*h_1(t) \\
&= x(t) * (h(t) * h_1(t))\\
&= x(t) * \delta(t) \\
&= x(t)
\end{align*}
$$

Therefore, we will calculate **inverse system** such that

$$
h[n]*h_1[n] = \delta[n]\\
h(t)*h_1(t) = \delta(n)
$$

As the resulting serial system, $$h(t)*h_1(t)  = \delta(t)$$ is memoryless.

The concept of inverse system is widely used for filtering out the noise and recvover the original signal $$x(t)$$ . If we can find a inverse system $$h_1(t)$$ of the noise $$h(t)$$, then we can obtain orignal signal $$x(t)$$ from the noisy signal $$y(t)$$.

## Accumulator System

Consider an system with an impulse response $$h[n] = u[n]$$.
By convolution, the response to an arbitrary input $$x[n]$$ is computed by

$$
y[n] = x[n]*h[n] = \sum_{k=-\infty}^{\infty}x[k]h[n-k]
$$

As $$h[n-k] = 1$$ only if $$k \le n$$, the given sum can be expressed as

$$
y[n] = \sum_{k=-\infty}^{n}x[k]
$$

Then, the inverse system can be expressed as $$y[n] = x[n] - x[n-1]$$ .

- Why $$y[n] = x[n]-x[n-1]$$ is an inverse system?
  The accumulator system can be expressed as $$y[n] -y[n-1] = x[n]$$ . Suppose an system
  $$
  x[n] \rightarrow \boxed{h[n]} \rightarrow  y[n] \rightarrow \boxed{h_1[n]} \rightarrow w[n]
  $$
  Then, it is clear that $$w[n] =y[n]-y[n-1] =x[n]$$ is the inverse system.
  Therefore, $$y[n] = x[n]-x[n-1]$$ is the inverse system of the accumulator.

The impulse response of an inverse system $$h_1[n]$$ is obtained by letting input signal $$x[n]$$ be $$\delta[n]$$.

$$
h_1[n] = \delta[n] - \delta[n-1]
$$

Then, by definition, $$x[n] * h[n] * h_1[n]$$ must be equivalent to $$x[n]$$ ,

$$
\begin{align*}
x[n]*h[n]*h_1[n] &= x[n] * (u[n] * (\delta[n]-\delta[n-1])\\
&= x[n]*\sum_{k=-\infty}^{\infty}u[n-k](\delta[k]-\delta[k-1])\\
&= x[n]*\sum_{k=-\infty}^{n}(\delta[k]-\delta[k-1])\\
&= x[n]*\delta[n] = x[n]
\end{align*}
$$

We’ve checked that $$h_1[n]=\delta[n] -\delta[n-1]$$ is an impulse response of an inverse system of accumulator

## Causality

Causal system only depends on present and past values of the input signal. Let’s take a look into the form of the convolution.

$$
y[n] = \sum_{k = -\infty}^{\infty}x[k]h[n-k]
$$

It can be easily seen that if $$k > n$$, then $$y[n]$$ depends on the future input $$x[k]$$. Therefore, $$h[n-k]  =0$$ for all $$k > n$$ or, $$h[n] = 0$$ for $$n< 0$$. It leads to some conclusion,

$$
y[n] = x[n]*h[n] = \sum_{k=-\infty}^{n}x[k]h[n-k]\\
y(t)=x(t)*h(t) = \int_{-\infty}^{t}x(\tau)h(t-\tau)d\tau
$$

## Stability

A system is **stable** if every bounded input produces a bounded output (BIBO). Consider a bounded input signal $$\|x[n]\| < B$$ for all $$n.$$ Then,

$$
\begin{align*}
\|y[n]\| &= \bigg\|\sum_{k=-\infty}^{\infty}x[n-k]h[k]\bigg\|\\
&\le \sum_{k=-\infty}^{\infty}\|x[n-k]\|h[k]\| \;\; \text{(triangle inequality)}\\
&\le B\sum_{k = -\infty}^{\infty}\|h[k]\|
\end{align*}
$$

Therefore, LTI system is stable if and only if its impulse response it absolutely summable, that is,

$$
\sum_{k=-\infty}^{\infty}\|h[k]\| < \infty \;\; \int_{-\infty}^{\infty}\|h(\tau)\|d\tau < \infty
$$

# Difference and Differential Equations

Some causal LTI systems can be described by **********\***********linear, constant-coefficient, ordinary differential/difference equations,\*

$$
\frac{dy(t)}{dt} + ay(t) = bx(t)\\
y[n] + ay[n-1] = bx[n]
$$

To solve these equations, we need to know the initial conditions.

In continuous time, if $$a > 0$$, then the system is unstable (exponential growth)

In discrete time, if $$a > 1$$, then the system is unstable.

## Differential Equations in Continuous Time

Consider a first-order differential equation and the input signal of

$$
\frac{dy(t)}{dt} +2y(t) = x(t) \\
x(t) = Ke^{3t}u(t) \; (K\in \mathbb{R})
$$

A complete solution of the equation is the sum of particular and homogeneous solution, that is, $$y(t) = y_h(t) + y_p(t)$$

### Particular Solution

As $$x(t) = Ke^{3t}$$, let $$y_p(t) = Ye^{3t}$$ for $$t \ge 0$$. Then,

$$
3Ye^{3t}+2Ye^{et} = 5Ye^{3t}= Ke^{3t} \rightarrow Y = \frac{1}{5}K
$$

Therefore, we have

$$
y_p(t) = \frac{K}{5}e^{3t}u(t)
$$

### Homogeneous Solution

Now assume our homogeneous solution $$y_h$$ be $$y_h = Ae^{st}$$. Then,

$$
\frac{d}{dt}y_h + 2y_h = Ase^{st}+2Ae^{st} = 0 \rightarrow s =-2
$$

Now we have homogeneous solution of $$y_h(t) = Ae^{-2t}$$

### Complete Solution

As we computed the homogeneous solution and paritcular solution, we are ready to compute the complete solution,

$$
y(t) = Ae^{-2t}+\frac{K}{5}e^{3t} \;\;\ (t>0)
$$

Now, assume the system is causal. That is, $$y(t) = 0$$ for $$t\le 0$$.

$$
y(0) = A + \frac{K}{5} = 0 \rightarrow A = -\frac{K}{5}
$$

Therefore, the complete solution can be expressed as

$$
y(t) = \bigg(-\frac{K}{5}e^{-2t}+\frac{K}{5}e^{3t}\bigg)u(t)
$$

## Difference Equations in Discrete Time

Consider a diffrential equation and input signal of

$$
y[n]-\frac{1}{2}y[n-1]=x[n]\\
x[n] = k\delta[n]
$$

As $$x[n]=0$$ for $$n \le -1$$, $$y[ n]=0$$ for $$n\le -1$$.

Now we will solve with by the induction.

$$
y[0] = x[0] + 0 = k \\
y[1] = x[1] + \frac
{1}{2}k = \frac{1}{2}k\\
y[2] = x[2] + \frac{1}{4}k = \frac{1}{4}k\\
\vdots\\
y[n] = \big(\frac{1}{2}\big)^n k \;\;\ (n \ge0)
$$

Therefore the solution is $$y[n] = \big(\frac{1}{2}\big)^n\times u[n]$$
