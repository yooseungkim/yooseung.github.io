---
layout: post
title:
tags: [Signals-and-Systems]
permalink: /2023-spring/signals-and-systems/convolution-in-dt
---

# Convolution in D.T.

## Convolution

**Convolution** is an operator that takes an input signal and returns an output signal, based on knowledge about the system’s **unit impulse response** $$h[n]$$

$$
x[n]=\delta[n]\rightarrow \boxed{\text{system}} \rightarrow h[n]\\
x[n] \rightarrow \boxed{\text{system}: h[n]}\rightarrow y[n]
$$

The system’s response to complex signals can be cacluated with simple input signals, such as unit impulse function $$\delta[n]$$. It is possible for all LTI systems, since they posses superposition properties

If the input signal is $$\delta[n]$$, then we know how system responses to the signal, a kick at $$n=0$$. This response is so common, so we use $$h[n]$$ to denote the output signal, instead of $$y[n]$$. And the system can be inferred with its parameter $$\theta$$ .

$$
\delta[n] \rightarrow \boxed{\text{system}:\theta} \rightarrow h[n]
$$

## Mathematical Definition

Any input signal can be represented as a infinite set of discrete time impulses. Any discrete input signal $$x[n]$$ at can be decomposed to the sum of $$x[k]\delta[n-k]$$, since

$$
x[k] : \text{actual value of}\; x[n]\; \text{at}\; n=k\\
\delta[n-k] = \begin{cases}0\; (n \neq k)\\
1\; (n=k)\end{cases}
$$

Therefore, any discrete signal can be represented as linear combination of $$x[k]\delta[n-k]$$, i.e.,

$$
x[n]= \sum_{k=-\infty}^{\infty}x[k]\delta[n-k]
$$

It is obvious that $$x[0] = \dots+x[-1]\delta[1]+x[0]\delta[0]+x[1]\delta[-1] = x[0]\delta[0]$$ $$(\because \delta[0]=1)$$

### Example

For example, consider a input signal $$x[n] = [0,\ 1,\ 2,\ 3,\ 1]$$, starting from $$n=0$$. Then, it can be decomposed to

$$
0\times \delta[n]+1\times \delta[n-1] + 2\times \delta[n-2]+3\times \delta[n-3] + 1\times \delta[n-4]
$$

We can easily compute that,

$$
\begin{align*}
&x[0]=0\times\delta[0]=0,\; x[1]=1\times\delta[0]=1\\
&x[2]=2\times\delta[0]=2,\; x[3]=3\times\delta[0]=3\\
&x[4]=1\times\delta[0]=1,
\end{align*}
$$

and the result is consistent with origincal input signal $$x[n]$$.

## Linear, Time Varying Systems

If the system is time varying, then the unit impulse response is time varying. That is, we cannot express the impulse response as $$h[n]$$. Therefore, let $$h_k[n]$$ denote the response to the impulse signal $$\delta[n-k]$$. Although it is time varying, it possesses linear propery, so general input $$x[n]$$ can be expressed as

$$
x[n]=\sum_{k=-\infty}^{\infty}x[k]\delta[n-k]
$$

Also, system output signal is given by **convolutional sum,** i.e., scaled sum of impulse responses

$$
y[n]=\sum_{k=-\infty}^{\infty}x[k]h_k[n]
$$

### Example

For example, let input signal $$x[n]$$ and time-varying impulse response $$h_k[n]$$ be

$$
\begin{align*}&x[n] = [0\ 0\ -1\ 1.5\ 0]\;\; \text{starting from}\; n=-3\\
&h_{-1}[n] = [0\ 0\ -1.5\ -0.7\ 0.4]\\
&h_0[n] = [0\ 0\ 0\ 0.5\ 0.8]
\end{align*}
$$

Let assume $$h_k[n] = 0$$ for $$k\neq -1,\ 0$$. Then, we take convolutional sum to get output signal

$$
\begin{align*}
y[n] &= \sum_{k=-\infty}^{\infty}x[k]h_k[n]\\
&= \dots+ x[-1]h_{-1}[n]+x[0]h_0[n]+\cdots\\
&= -1\times [0\ 0\ -1.5\ -0.7\ 0.4]\\
&+ 1.5\times [0\ 0\ 0\ 0.5\ 0.8]\\
&= [0\ 0\ 1.5\ 1.45\ 0.8]
\end{align*}
$$

## Linear Time Invariant (LTI) Systems

If the system is time-invariant, then the unit impulse response are time-shifted versions of each other. In other words, shifting $$h_0[n]$$ with $$k$$ units make response for delayed $$k$$ units.

$$
h_k[n] = h_0[n-k]
$$

Therefore, the unit impulse response for LTI system can be represented with $$h_0[n]$$ and usually we simply define it as

$$
h[n] =h_0[n]
$$

In this case, we can simply compute **convolution sum** for LTI system by

$$
y[n]=x[n]\ast h[n]=\sum_{k=-\infty}^{\infty} x[k]h[n-k]
$$

## Identification and Prediction

We know verified that system’s response to arbitrary input signal is determined by its response to the unit impulse response $$h[n]$$, due to convolution. This means that if we can compute $$h[n]$$, then we can compute response to any other arbitrary input signal.

Therefore, we first **identify** a particular LTI system by applying $$\delta[n]$$ and measure the $$h[n]$$.

$$
x[n]=\sum_{k=-\infty}^{\infty}x[k]\delta[n-k]
$$

Then, by using $$h[n]$$, we can **predict** the system’s response $$y[n]$$ to any input signal $$x[n]$$.

$$
y[n]=\sum_{k=-\infty}^{\infty}x[k]h[n-k]
$$

- There is a direct mapping between $$y[n]$$ and $$h[n]$$, such as $$y[n]=x[n]+0.5x[n-1]$$

## Examples

### Example 1

Consider a LTI system with following impulse response and input signal starting from $$n=-2$$

$$
h[n]=[0\ 0\ 1\ 1\ 1\ 0\ 0]\\
x[n]=[0\ 0\ 0.5\ 2\ 0\ 0\ 0]
$$

The response to $$x[n]$$ can be computed as

$$
\begin{align*}
y[n] &= \sum_{k=-\infty}^{\infty}x[k]h[n-k]\\
&= \dots+x[0]h[n]+x[1]h[n-1]+x[2]h[n-2]+\cdots\\
&= 0.5 \times [0\ 0\ 1\ 1\ 1\ 0\ 0]\cdots\ \cdots (1)\\
&+ 2 \times [0\ 0\ 0\ 1\ 1\ 1\ 0]\cdots\ \cdots (2)\\
&= [0\ 0\ 0.5\ 2.5\ 2.5\ 2\ 0]
\end{align*}
$$

Note that $$(2)=h[n-1]$$ is signal obtained by shifting $$+1$$ unit from $$(1)=h[n]$$

### Example 2

Consider a LTI system in **Example 1**.

For each particular $$n$$, we can consider some graphs as following.

![Untitled](Convolution%20in%20D%20T%20bf7a7a636bbe42a19e943f507e556fe3/Untitled.png)

- For $$n< 0$$, there is no overlap, so $$y[n]=0$$
- $$n=0$$, then it overlaps at $$k=0$$.
  - $$y[0]=x[0]h[0] = 0.5$$
- $$n=1$$, then it overlaps at $$k=0, 1$$
  - $$y[1] =x[1]h[1]+x[0]h[0]=0.5$$
- $$n=2$$, then it overlaps at $$k=0,1$$
  - $$y[2]=0.5$$
- $$n=3$$, then it overlaps at $$k=1$$
  - $$y[3]=x[1]h[1]=2$$
- For $$n>0$$, there is no overlap, so $$y[n]=0$$

The result is consistent with **Example 1**.

### Example 3

Consider a LTI system with following unit impulse response and input signal

$$
h[n]=u[n]=\begin{cases}0\; (n<0)\\ 1\; (n\ge0)\end{cases}\\
x[n]=\alpha^nu[n]\;(0<\alpha<1)
$$

We can compute the response $$y[n]$$ on $$n \ge 0$$ to the input signal by

$$
\begin{align*}
y[n] &=\sum_{k=-\infty}^{\infty}x[k]h[n-k]\\
&=\sum_{k=0}^{\infty}\alpha^k\; \big(\because n \ge0 \rightarrow u[n-k] = \begin{cases}1\; (k \ge 0)\\ 0\; (k < 0)\end{cases}\big)\\
&= \frac{1-\alpha^{n+1}}{1-\alpha}
\end{align*}
$$

It is obvious that for $$y[n] = 0$$ for $$n < 0$$.

$$
k<0 \rightarrow x[k] = 0\\
k\ge 0 \rightarrow u[n-k] = 0  (\because n-k <0)
$$

Thus, $$x[k]u[n-k]= 0$$ for all $$k$$, therefore $$y[n]=\sum_{k=-\infty}^{\infty}x[k]u[n-k] = 0$$

Finally, now we have $$y[n]$$ for all $$n$$, with using unit step function.

$$
y[n] = \big(\frac{1-\alpha^{n+1}}{1-\alpha}\big)u[n]
$$

### Example 4

Consider a LTI system with

$$
x[n] =\begin{cases}1\;\;\; 0\le n\le 4\\0 \;\;\; \text{otherwise}\end{cases}\\
h[n] = \begin{cases}\alpha^n\;\;\; 0\le n\le 6\\0\;\;\; \text{otherwise} \end{cases}
$$

We will consider some overlaps for each range of $$n$$. Following graph will be helpful.

![Untitled](Convolution%20in%20D%20T%20bf7a7a636bbe42a19e943f507e556fe3/Untitled%201.png)

Note that $$h[n-k]$$ will be graphed on $$k-$$axis, not on $$n$$-axis. Therefore, $$h[n-k]$$ will be form of **flipped $$h[n]$$**.

The range of $$k$$ can be obtained by finding the overlapping range of two signals.

(i) $$n<0$$

Obviously, $$x[k]$$ and $$h[n-k]$$ do not overlap for $$n < 0$$. Thus $$y[n] = 0$$

(ii) $$0\le n \le 4$$

In this case, head $$(h[0])$$ overlaps with $$x[k]$$, but tail $$(h[6])$$ does not.

$$
x[k]h[n-k]=\begin{cases}\alpha^{n-k}\;\;&0 \le k \le n\\ 0\;\; &\text{otherwise}\end{cases}
$$

Therefore, the output response to the signal is

$$
y[n]=\sum_{k=0}^{n}\alpha^{n-k}=\frac{1-\alpha^{n+1}}{1-\alpha}
$$

(iii) $$4< n \le 6$$

In this case, the body of $$x[k]$$ overlaps with $$h[n-k]$$ .

$$
x[k]h[n-k]=\begin{cases}
\alpha^{n-k} &0 < k \le 4\\
0 &\text{otherwise}
\end{cases}
$$

Therefore, the output response to the signal is

$$
y[n]=\sum_{k=0}^{4}\alpha^{n-k} = \frac{\alpha^{n-4} - \alpha^{n+1}}{1-\alpha}
$$

(iv) $$6 < n \le 10$$
In this case, only the tail $$(h[0])$$ overlaps with $$x[k]$$

$$
x[k]h[n-k] = \begin{cases}
\alpha^{n-k} &n - 6 \le k \le 4\\
0 &\text{otherwise}
\end{cases}
$$

Therefore, the output response to the signal is

$$
y[n] =\sum_{k=n-6}^{4} \alpha^{n-k} = \frac{\alpha^{n-4}-\alpha^{7}}{1-\alpha}
$$

(v) $$n > 10$$

Obviously, there is no overlap, so $$y[n] = 0$$

From (i), (ii), (iii), (iv), and (v), we have $$y[n]$$ for all $$n$$
