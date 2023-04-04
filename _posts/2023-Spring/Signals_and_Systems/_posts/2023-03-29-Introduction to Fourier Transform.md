---
layout: post
title:
tags: [Signals-and-Systems]
permalink: /2023-spring/signals-and-systems/intro-to-fourier-transform
---

# Introduction to Fourier Transform

# Fourier Series

In the last lecture, we discussed Fourier series representation of periodic signal, which is a discrete set of complex coefficients. Recall that Fourier coefficient $$a_k$$ is given by

$$
x(t) = \sum_{k=-\infty}^{\infty}a_ke^{jk\omega_0t}\\
a_k = \frac{1}{T}\int_{T}x(t)e^{-jk\omega_0t}dt
$$

## Finite Fourier Series

In reality, Foureier series is defined as

$$
x_N(t) = \sum_{k=-N}^{N}a_ke^{jk\omega_0t}
$$

As $$N \rightarrow \infty$$, it is closely approximated to the original signal, that is, $$x_N(t) \rightarrow x(t)$$. But how do we determine such $$N$$?

We will set the tolerance $$\epsilon$$, and find the $$N$$ such that satisfies

$$
\int_{\infty}^{\infty} \|x(t) -x_N(t)\|^2dt < \epsilon
$$

## Convergence

All signals that we are interested in can be represented as an infinite Fourier series, but not every periodic signal can be. If the signal satisfies the **Dirichlet condition**, then it can be represented as an infinite Fourier series, and vice versa.

1. Over any period, $$x(t)$$ must be absolutely integrable, i.e. $$\int_T \|x(t)\|dt < \infty$$
2. In any finite interval, $$x(t)$$ is of bounded variation, only there are finite number of maxima and minima in a single period.
3. In any finite interval, $$x(t)$$ has only a finite number of discontinuities.

For example, $$x(t) = \frac{1}{t}  (0<t<1)$$ violates the condition 1 and $$x(t) = \sin(\frac{1}{t})$$ violates the condition 2.

For $$x(t) = \frac{1}{t}$$,

$$
\int_0^1 \frac{1}{t}dt = \ln t \big\|_=^1 = \infty
$$

For $$x(t) = \sin(1/t)$$, there are infinite number of vibration, therefore inifinite minima and maxima. Although it violates condition 2, it satisfies condition 1, since

$$
\int_0^{2\pi} \sin(1/t)dt < \infty
$$

## Properties of Fourier Coefficients

In fact, most of properties we have learned hold in Fourier coefficients

Let $$F$$ denote the transformation from $$f(t)$$ to the Fourier coefficeients.

### Linearity

$$
F(\alpha f(t)+\beta g(t)) = \alpha a_k+ \beta b_k
$$

It can be shown by just using the definition of Fourier coefficients.

### Time-shifting

$$
\begin{align*}
f(t-t_0)) &= \sum_k a_k e^{jk\omega_0 (t-t_0)}\\
&= \sum_k (e^{-jk\omega_0t_0}a_k )e^{jk\omega_0t}\\
\therefore F(f(t-t_0)) &= e^{-jk\omega_0t_0}a_k
\end{align*}
$$

### Time Reversal

It is very simple, just that

$$
x(t)  \rightarrow a_k \text{  then } x(-t)\rightarrow a_{-k}
$$

- Proof
  It can be easily shown by substituting $$-t$$ with $$t$$, that is,
  $$
  \begin{align*}
  x(-t) &= \sum_k a_k e^{jk\omega_0(-t)}\\
  &= \sum_k a_{-k}e^{jk\omega_0t}
  \end{align*}

  $$

### Conjugation

It is similar with the time reversal,

$$
x(t) \rightarrow a_k \text{  then }\overline{x(t)} \rightarrow \overline{a_{-k}} = a^*_{-k}
$$

- Proof
  $$
  \begin{align*}
  \overline{x(t)} &= \sum_k \overline{a_k e^{jk\omega_0t}}\\
  &= \sum_k \overline{a_k} e^{-jk\omega_0t}\\
  &= \sum_k \overline{a_{-k}} e^{jk\omega_0t}
  \end{align*}
  $$
  Note that $$jk\omega_0t$$ is purely imaginary ($$j$$ is imaginary unit), therefore $$\overline{jk\omega_0t} = -jk\omega_0t$$.

### Multiplication

Let $$F(x(t)) = a_k$$ and $$F(y(t)) = b_k$$. And let $$z(t) = x(t)y(t)$$. Then, k

$$
z(t) = \sum_k c_ke^{jk\omega_0t}\\
c_k = \frac{1}{T}\int_T x(t)y(t)e^{-jk\omega_0t}
$$

In fact, $$x(t)$$ and $$y(t)$$ may have different frequencies, but for computational ease, assume both have the frequency of $$\omega_0$$.

$$
\begin{align*}
c_k &= \frac{1}{T}\int_T\bigg(\sum_{n=-\infty}^{\infty}a_n e^{jn\omega_0t}\bigg)y(t)e^{-jk\omega_0t}dt\\
&= \sum_n a_n\bigg(\frac{1}{T}\int_T y(t) e^{-j(k-n)\omega_0t}dt\bigg)\\
&= \sum_n a_n b_{k-n} \;\;\ \text{(due to } -j(k-n)\omega_0t)
\end{align*}
$$

The form $$c_k = \sum_n a_n b_{k-n}$$ is the same form of **convolution**. Therefore, the multiplication in time-domain is equivalent to the convolution in frequency-domain (Fourier domain).

### Parseval’s Relation

It is the relation that the energy of the signal is preserved, which seems very natural.

$$
E = \frac{1}{T}\int_T \|f(t)\|^2dt = \sum_{k=-\infty}^{\infty}\|a_k \|^2
$$

- Proof
  $$
  \begin{align*}
  \int_T \|f(t)\|^2dt &=  \int_T f(t)*f(t) dt \\
  &= \int_T \bigg(\sum_n a_ne^{jn\omega_0t}\bigg)*\bigg(\sum_m a_m e^{jm\omega_0t}\bigg)dt\\
  &= \int_T \bigg(\sum_n a_ne^{jn\omega_0t}\bigg)*\bigg(\sum_m a^*_m e^{-jm\omega_0t}\bigg)dt\\
  &= \int_T (a_1e^{j1\omega_0t} + a_2e^{j2\omega_0t} + \cdots)(a_1^*e^{-j1\omega_0t} + a_2^*e^{-j2\omega_0t})dt\\
  &= \sum_n \sum_m a_na_m^* \int_T e^{j(n-m)\omega_0 t}dt\\
  &=\int_T (a_1a_1^*+a_2a_2^* + \cdots) dt\\
  &= \sum_n \|a_n\|^2 \times T \;\; (\text{only if } n = m)\\

  \end{align*}
  $$
  Note that if $$n \neq m$$, then $$\int_T e^{j(n-m)\omega_0t} dt = 0$$, therefore only the terms with $$n=m$$ survives, and $$a_na_n^* = \|a_n\|^2$$.
  ### Symmetry
  If $$f(t)$$ is even signal, then
  $$
  f(t) = f(-t) \rightarrow a_k = a_{-k}
  $$
  Also, if $$f(t)$$ is odd signal, then
  $$
  f(t) = -f(-t) \rightarrow a_k = -a_{-k}
  $$
  ### Conjugate Symmetry
  If $$f(t)$$ is purely real, then
  $$
  f(t) = f(t)^* \rightarrow a_k = a_{-k}^*
  $$
  Then, the coefficients are conjugate symmetry, that is,
  $$
  a_k = a_{-k}^* \\
  \Re\{a_k\} = \Re\{a_{-k}^*\}\\
  \Im\{a_k\} = \Im\{a_{-k}^*\}\\
  \|a_k\| = \|a_{-k}^*\|\\
  angle\{a_k\} = angle\{a_{-k}^*\}
  $$
  ### Differentiation and Integration
  As $$f(t) = \sum_k a_k e^{jk\omega_0t}$$, $$\frac{df(t)}{dt} = \sum_k jk\omega_0a_k e^{jk\omega_0t}$$. Therefore,
  $$
  F(\frac{df(t)}{dt}) = jk\omega_0a_k
  $$
  It can be observed that the high frequencies are emphasized, due to $$\omega_0$$ term.
  On the other hand, similar to differentiation,
  $$
  F\bigg(\int_{-\infty}^t f(\tau)d\tau\bigg) = \frac{1}{j\omega_0k}a_k
  $$
  Thus, integration emphasizes the low frequencies.

# Fourier Transform

From now on, we will extend our discussion to **non-periodic signals**. We will consider non-periodic signal as a periodic signal with infinite period. As period becomes infinite, the corresponding frequency reaches zero ($$\because \omega = 2\pi/T)$$ therefore the sum of Fourier series becomes an integral.

## Definition

A signal $$x(t)$$ and its Fourier transform $$X(j\omega)$$ are related by the Fourier transform synthesis,

$$
X(j\omega)= \int_{-\infty}^{\infty}x(t) e^{-j\omega t} dt = F\{x(t)\}\\
x(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty}X(j\omega)e^{j\omega t}d\omega = F^{-1}\{X(j\omega\}
$$

A pair $$x(t)$$ and $$X(j\omega)$$ are called a **Fourier transform pair** and denoted by

$$
x(t) \overset{F}{\leftrightarrow}X(j\omega)
$$

The transform function $$X$$ can be considered as a continuum of the coefficients.

## Examples

### Example 1

Consider non-periodic signal $$x(t) = e^{-at}u(t)$$

Its Fourier transform is given by

$$
\begin{align*}
X(j\omega) &= \int_0^\infty e^{-at}e^{-j\omega t}dt \\
&= \int_0^\infty e^{-(a+j\omega)t}dt\\
&= \frac{1}{a+j\omega}
\end{align*}
$$

### Example 2: Rectangular Pulse

Consider non-periodic rectangular pulse at zero, that is,

$$
x(t) = \begin{cases}
1 & \|t\| <T_1 \\
0 & \|t\| \ge T_1\end{cases}
$$

Its Fourier transform is given by

$$
\begin{align*}
X(j\omega) &= \int_{-\infty}^{\infty}x(t)e^{-j\omega t}dt \\
&= \int_{-T_1}^{T_1} e^{-j\omega t} dt \\
&= -\frac{1}{j\omega}(e^{-j\omega T_1} - e^{j\omega T_1})\\
&= 2 \frac{1}{2j\omega}(e^{j\omega T_1} - e^{-j\omega T_1}) \\
&= \frac{2\sin(\omega T_1)}{\omega}
\end{align*}
$$

Therefore, the Fourier transform of rectangular pulse is a **sinc function**.

### Example 3: Impulse Signal

Consider an impulse function $$x(t) = \delta(t)$$

Then, its Fourier transform is

$$
X(j\omega) = \int_{-\infty}^{\infty}\delta(t)e^{-j\omega t} dt = e^{-j\omega 0} = 1
$$

Therefore, the Fourier transform of the impulse function is a constant in frequency domain.

### Example 4: Periodic Signal

A periodic signal violates the condition 1 of the DIrichlet conditions since

$$
\int_T \|f(t)\|dt = k \rightarrow \int_{-\infty}^{\infty} \|f(t)\|dt = \infty
$$

But consider a Fourier transform which is a single impulse of the interval $$2\pi$$ at a frequency of $$\omega = \omega_0$$. Then,

$$
X(j\omega) = 2\pi \delta(\omega - \omega_0)
$$

Then the original signal can be obtained by an inverse Fourier transform,

$$
x(t) = \frac{1}{2\pi}\int_{-\infty}^{\infty}2\pi\delta(\omega-\omega_0)e^{j\omega t} d\omega = e^{j\omega_0t} \; (\omega = \omega_0)
$$

As $$e^{j\omega_0t} = \cos\omega_0t + j\sin\omega_0 t$$, it is a sinusoidal signal of frequency $$\omega_0$$.

In general, if $$X(j\omega) = \sum_k 2\pi a_k \delta(\omega - k\omega_0)$$, then its corresponding periodic signal is

$$
x(t) = \sum_{k=-\infty}^{\infty}a_ke^{jk\omega_0t}
$$

Therefore, the Fourier transform of a periodic signal is a train of impulses at the harmonic frequencies with amplitude $$2\pi a_k$$. That is,

$$
X(j\omega) = 2\pi a_1(\omega - \omega_1) + 2\pi a_2(\omega - \omega_2) + \cdots\\
= \begin{cases}
1 &\omega = k\omega_0\\
0 &\omega \neq k\omega_0
\end{cases}
$$
