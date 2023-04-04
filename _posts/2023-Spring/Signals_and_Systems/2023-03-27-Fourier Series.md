---
layout: post
title:
tags: [Signals-and-Systems]
permalink: /2023-spring/signals-and-systems/fourier-series
---

# Fourier Series

# Eigen Functions

A prefiex **_eigen-_** means its own or representative. For a particular system, there would be some signal $\phi_k(t)$ with the property of

$$
x(t)=\phi_k(t) \rightarrow \boxed{\text{system}}\rightarrow y(t) = \lambda_k\phi_k(t)
$$

Then, we call $\phi_k(t)$ is an **eigenfunction** with the **eigenvalue** $\lambda_k$.
For an LTI system, since the superposition can be applied, therefore

$$
x(t) =\sum_k a_k\phi_k(t) \rightarrow y(t) = \sum_ka_k\lambda_k\phi_k(t)
$$

Also, $\phi_k(t) = e^{st}\; (s\in \mathbb{C})$ are eigenfucntions for an LTI system.

# Fourier Series

## Importance

Fourier transform maps a time-domain signal into a frequency-domain signal. It helps filter out high or low frequency componenents, since high frequency signals are usually noises.

Let $X(jw)$ be the Fourier transform of $x(t)$, that is, $F\{x(t)\} = X(jw)$ and then,

$$
F\{x'(t)\}=jwX(jw)
$$

Therfore, we can solve a differerential equation with an algebraic operation, not calculus operation. (It is similar with Laplace transform)

Now consider a LTI system,

$$
x(t) =\sum_k a_k\phi_k(t) \rightarrow y(t) = \sum_ka_k\lambda_k\phi_k(t)
$$

We will first **identify** the system by finding $\phi_k(t)$ and $\lambda_k$.
Then, we will find the coefficients $a_k$ to find the system **response**.

## Eigenvalue

Consider a LTI system with impulse response $h(t)$ and input signal $x(t) = \phi(t) = e^{st}$. Then,

$$
\begin{align*}
y &= \int_{-\infty}^{\infty} h(\tau)x(t-\tau)d\tau\\
&= \int_{-\infty}^{\infty} h(\tau)e^{s(t-\tau)}d\tau\\
&= e^{st} \int_{-\infty}^{\infty} h(\tau)e^{-s\tau}d\tau\\
&= \int_{-\infty}^{\infty} h(\tau)e^{-s\tau}d\tau \times \phi(t)
\end{align*}
$$

Therefore, $\phi(t) = e^{st}$ is an eigenfunction with an eigenvalue $\lambda = H(s) = \int_{-\infty}^{\infty} h(\tau)e^{-s\tau}d\tau$.

### Example 1: Time Delay

Consider a LTI system $y(t) = x(t-3)$

As $x(t) * \delta(t-3) = x(t-3)$, the system response $h(t) = \delta(t-3)$. Now, we can compute the eigenvalue $H(s)$ corresponding to eigenfunction $e^{st}$ by

$$
H(s) = \int_{-\infty}^{\infty}\delta(\tau-3)e^{-s\tau}d\tau = e^{-3s}
$$

For example, if the input signal is given by $x(t) = e^{j2t}$, then $s = j2$, so $H(j2)=e^{-j6}$.

### Example 2: Phase Shift

Note that $H(s) = e^{-3s}$. Consider an input signal of $\cos(2t)$, which can be represented as

$$
\cos(2t) = \frac{1}{2}(e^{j2t}+e^{-2jt})
$$

By the LTI property of the system,

$$
\begin{align*}
y(t) &= \frac{1}{2}(H(2j)e^{2jt} + H(-2j)e^{-2j})\\
&= \frac{1}{2}(e^{2j(t-3)}+e^{-2j(t-3)})\\
&= \cos(2(t-3))
\end{align*}
$$

As the eigenvalue is purely imaginary, it corresponds to a **phase shift** of the system’s response. The real component of the eigenvalue would change the amplitude of the signal.

## Periodic Signals and Fourier Series

Any input signals can be represented as a linear combination (superposition) of a basis function, that is, complex exponentials, which can be represented as scaled and shifted sinusoidal signals. As more and more basis functions are combined, the error between the orignal signal decreases.

If a periodic signal has the property $x(t) = x(t+T)$, $T$ is the **fundamental period** and $\omega_0 =2\pi/T$ is the **fundamental** **frequency**. For example,

$$
x(t) = cos(\omega_0t), \; x(t) = e^{j\omega_0t}
$$

The **Fourier basis** is the set of harmonically related complex exponentials, i.e.,

$$
\phi_k(t) = e^{jk\omega_0t} = e^{jk\frac{2\pi}{T}t} \; (k = 0, \pm1,\ \pm2,\dots)
$$

Therefore, the Fourier series is of the form

$$
x(t) = \sum_{k=-\infty}^{\infty}a_ke^{jk\omega_0t}
$$

## Fourier Coefficients

We have derived that the input signal $x(t)$ can be expressed as the linear combination of the Fourier basis function $\phi_k(t)$. Now we need to find the Fourier coefficient $a_k$.

First, multiply $e^{-jn\omega_0t}$ on both sides. Then we have

$$
\begin{equation}
x(t)e^{-jn\omega_0t} = \sum_{k=-\infty}^{\infty} a_k e^{j(k-n)\omega_0t}
\end{equation}
$$

And integrate from 0 to $T$ (or any interval of length $T$)

$$
\begin{equation}
\int_{0}^{T}x(t)e^{-jn\omega_0t}=\sum_{k=-\infty}^{\infty}a_k\int_{0}^{T}e^{j(k-n)\omega_0t}
\end{equation}
$$

Using Euler’s formula,

$$
\int_0^Te^{j(k-n)\omega_0t} = \int_0^T \cos((k-n)\omega_0t)dt + j\int_0^T\sin((k-n)\omega_0t)dt\\
= \begin{cases}
T &k=n\\
0 &k\neq n
\end{cases}
$$

If $k \neq n$, then $\sin(k-n)\omega_0t$ has the frequency of $2\pi/(k-n)\omega_0 = T/(k-n)$. Then, integrating from $0$ to $T$ must be equal to zero, since $T$ is multiple of its frequency.

Now, from

$$
\int _0^T x(t)e^{-jn\omega_0t}dt = a_nT
$$

we have $a_n = \frac{1}{T}\int_0^Tx(t)e^{-jn\omega_0t}dt$.

In general, we can express the Fourier coefficient with interval $T$,

$$
a_k= \frac{1}{T}\int_T x(t)e^{-jk\omega_0t}dt
$$

### Example 1

Find the Fourier coefficients of $\sin(\omega_0t)$

The fundamental period of the signal is $2\pi/\omega_0$.

$$
a_0=\frac{1}{T}\int_0^T \sin(\omega_0t) dt = -\frac{\omega_0}{2\pi}\cos(\omega_0t) \big|_0^{2\pi/\omega_0} = 0
$$

$$
\begin{align*}
a_k &= \frac{1}{T}\int_0^T \sin(\omega_0t)e^{-jk\omega_0t}dt \\&=\frac{1}{T}\int_0^T (\frac{1}{2j}e^{j\omega_0t}-\frac{1}{2j}e^{-j\omega_0t})e^{-jk\omega_0t}dt\\
&= \frac{\omega_0}{4\pi j} \int_{0}^{2\pi/\omega_0} e^{-j(k-1)\omega_0t}-e^{-j(k+1)\omega_0t}dt\\
\end{align*}
$$

If $k = 1$ , then $a_1  = \frac{\omega_0}{4\pi j}\times 2\pi/\omega_0 = \frac{1}{2j}$, and if $k=-1,$ $a_{-1} =-\frac{1}{2j}$. However, if $k\neq\pm1$, then $a_k=0$, since the integrand is periodic.

### Example 2

A periodic square wave is defined over one period as

$$
x(t) = \begin{cases}
1& |t|<T_1\\
0& T_1 < |t| < \frac{T}{2}
\end{cases}
$$

First compute $a_0$. For computational ease, let $T = 2T_1$.

$$
a_0 = \frac{1}{T} \int_{T_1}^{T_1}1dt = 1
$$

Then compute the $a_k$ for nonzero $k$

$$
a_k = \frac{1}{T}\int_{-T_1}^{T_1}e^{-jk\omega_0t}dt = \frac{2}{k\omega_0T}\big(\frac{e^{jk\omega_0T_1}-e^{-jk\omega_0T_1}}{2j}\big) = \sin(k\omega_0T_1)/k\pi
$$

Note that $a_k$ is of the **sinc function** form. That is, it is of the form

$$
\frac{\sin(x)}{x}
$$

The importance of rectangular signal and the sinc function will be discussed on the next lecture.
