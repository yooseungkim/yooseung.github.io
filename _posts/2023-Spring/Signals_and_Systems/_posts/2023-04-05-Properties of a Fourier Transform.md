---
layout: post
title: Properties of a Fourier Transform
tags: [Signals-and-Systems]
permalink: /2023-spring/signals-and-systems/properties-of-ft
---

# Properties of a Fourier Transform

# Properties

Recall a Fourier transform, a signal $$x(t)$$ and its fourier tranform $$X(jw)$$ are related by

$$
x(t) = \frac{1}{2\pi}\int_{-\infty}^{\infty}X(j\omega)e^{j\omega t}d \omega \\
X(j\omega) = \int_{-\infty}^{\infty}x(t)e^{-j\omega t}dt
$$

Also, a Fourier transform for $$e^{-at}u(t)$$ is given by

$$
\begin{align*}
\mathcal{F}[e^{-at}u(t)] &= \int_{-\infty}^{\infty}e^{-at}u(t)e^{-j\omega t}dt \\
&= \int_{0}^{\infty}e^{-(a+j\omega)t}dt\\
&= \frac{-1}{a+j\omega}e^{-(a+j\omega)t}\bigg\|_{0}^{\infty}\\
&= \frac{1}{a+j\omega}
\end{align*}
$$

## Linearity

As integral operator is linear, it is clear that Fourier transform is linear. That is, if

$$
x(t)\overset{\mathcal{F}}\leftrightarrow X(j\omega), \;\; y(t) \overset{\mathcal{F}}\leftrightarrow  Y(j\omega)
$$

Then,

$$
ax(t)+by(t) \overset{\mathcal{F}}\leftrightarrow aX(j\omega) + bY(\omega)
$$

Therefore, the superposition property holds.

## Time shifting

Let $$x(t)\overset{\mathcal{F}}\leftrightarrow X(j\omega)$$. Then, the Fourier transform of the time shifted signal $$x(t-t_0)$$ is given by

$$
\begin{align*}
x(t-t_0) &=\frac{1}{2\pi} \int_{-\infty}^{\infty}X(j\omega)e^{j\omega(t-t_0)}d\omega\\
&= \frac{1}{2\pi}e^{-j\omega t_0}\int_{-\infty}^{\infty}X(j\omega)e^{j\omega t}d\omega \\\\
&\therefore \mathcal{F}[x(t-t_0)] = e^{-j\omega t_0}X(j\omega)
\end{align*}
$$

## Differentiation and Integration

A Fourier transform is of the form $$x(t) = \frac{1}{2\pi}\int_{-\infty}^{\infty}X(j\omega)e^{-j\omega t}d \omega$$.
Then, differentiating boths sides with respect to $$t$$ gives

$$
\frac{dx(t)}{dt} = \frac{1}{2\pi}\int_{-\infty}^{\infty}j\omega X(j\omega)e^{j\omega t}d\omega
$$

Therefore, the differentiation in time domain is equivalent to the multiplication in frequency domain. That is,

$$
\frac{dx(t)}{dt} \overset{\mathcal{F}}\leftrightarrow  j\omega X(j\omega)
$$

Also, similar property holds for the integration,

$$
\begin{align*}
\mathcal{F}[\int_{-\infty}^{t}x(\tau)d\tau] &= \int_{-\infty}^{\infty}\int_{-\infty}^{t} x(\tau)d\tau e^{-j\omega t} dt\\
&= \int_{-\infty}^{\infty}\int_{-\infty}^{\infty}x(\tau)u(t-\tau)d\tau e^{-j\omega t}dt\\
&= \int_{-\infty}^{\infty}x(\tau)\int_{\tau}^{\infty}u(t-\tau)e^{-j\omega t}dt d\tau\\
&= \int_{-\infty}^{\infty} \frac{1}{j\omega}x(\tau)e^{-j\omega \tau}d\tau\\
&= \frac{1}{j\omega}X(j\omega) \;\;(\omega \neq 0)
\end{align*}
$$

It is what we expected form, but $$\omega = 0$$ is a troubleshooting case. If $$\omega  = 0$$, which means it is DC with a amplitude of average value. Therefore,

$$
\begin{align*}
\mathcal{F}\bigg[\int_{-\infty}^{t}x(\tau)d\tau\bigg] = \pi X(0)
\end{align*}
$$

Combining these two, we have

$$
\begin{align*}
\mathcal{F}\bigg[\int_{-\infty}^{t}x(\tau)d\tau\bigg] = \frac{1}{j\omega}X(j\omega) + \pi X(0)\delta(\omega)
\end{align*}
$$

- Example: Step signal and Impulse function
  Let $$x(t) = u(t)$$ and $$g(t) = \delta(t)$$. Note that

  $$
  x(t)= u(t) = \int_{-\infty}^{t}g(\tau)d\tau\\g(t) =\delta(t) \overset{F}{\leftrightarrow}G(j\omega)=1


  $$

  Due to integration rule,

  $$
  X(j\omega) = \mathcal{F}[\int_{-\infty}^{t}g(\tau)d\tau] = \frac{G(j\omega)}{j\omega} + \pi G(0)\delta(\omega)
  $$

  As $$G(j\omega) = \int_{-\infty}^{\infty}\delta(t)e^{-j\omega t} dt = 1$$,

  $$
  X(j\omega) = \mathcal{F}[u(t)]=\frac{1}{j\omega} + \pi\delta(\omega)
  $$

  Also, in reverse, by applying differentiation property,

  $$

  \mathcal{F}[\delta(t)] = \mathcal{F}[\frac{du(t)}{dt}] = j\omega X(j\omega) \\= j\omega(\frac{1}{j\omega}+\pi\delta(\omega))=1\;\; (\because \omega\delta(\omega) = 0  \;\;\forall \omega)
  $$

  The result is consist with our previous knowledge.

## Time and Frequency Scaling

Let $$\mathcal{F}[x(t)] = X(j\omega)$$ then, by definition,

$$
\begin{align*}
\mathcal{F}[x(at)] &= \int_{-\infty}^{\infty}x(at)e^{-j\omega t}dt \\
&= \int_{-\infty}^{\infty}x(\tau)e^{-j\omega \frac{\tau}{a}}\frac{1}{\|a\|}d\tau\;\;(\tau = at)\\
& = \frac{1}{\|a\|}X(\frac{j\omega}{a})
\end{align*}
$$

Note that if $$a< 0$$, the range of integration changes from $$(-\infty,\infty)$$ to $$(\infty, -\infty)$$, therefore negative sign comes out. Therefore, we have

$$
\mathcal{F}[x(at)] = \begin{cases}
\frac{1}{a}X(\frac{j\omega}{a}) & a > 0\\\\
-\frac{1}{a}X(\frac{j\omega}{a}) & a < 0\end{cases}
$$

Also, letting $$a=-1$$, we can observe the time reversal, that is,

$$
x(-t) \overset{F}{\leftrightarrow} X(-j\omega)
$$

## Duality

A **duality** is two signals can be obtained by Fourier transform of each other. For example, we have shown that the Fourier transform of the rectangular pulse is sinc function. }

$$
X(j\omega) = \int_{-T_1}^{T_1}e^{-j\omega t}dt = \frac{2\sin(\omega T_1)}{\omega}
$$

By duality, the Fourier transform of sinc function is a rectangular pulse. Let $$y(t) = \frac{\sin Wt}{\pi t}$$. Then, its $$Y(j\omega)$$ is rectangular pulse,

$$
Y(j\omega) =\begin{cases}
1 &\|w\| < W\\
0 &\|w\| > W
\end{cases}
$$

# Convolution in Frequency Domain

One of the most important property of Fourier transform is the **convolution** in the frequency domain.

First, let $$y(t) = x(t) * h(t)$$, and take Fourier tranform. Then,

$$
y(t) = \int_{-\infty}^{\infty}x(\tau)h(t-\tau)d\tau\\
Y(j\omega) = \int_{-\infty}^{\infty}\int_{-\infty}^{\infty}x(\tau)h(t-\tau)d\tau e^{-j\omega t}dt
$$

By changing the order of integration, we have

$$
\begin{align*}
Y(j\omega) &= \int_{-\infty}^{\infty} \int_{-\infty}^{\infty}x(\tau)h(t-\tau)d\tau e^{-j\omega t}dt\\
&= \int_{-\infty}^{\infty} x(\tau)\int_{-\infty}^{\infty}h(t-\tau)e^{-j\omega(t-\tau)}dt \:e^{-j\omega\tau} d\tau\\
&= \int_{-\infty}^{\infty}x(\tau)H(j\omega)e^{-j\omega t}d\tau\\
&= X(j\omega)H(j\omega)
\end{align*}
$$

Therefore, we have $$Y(j\omega)=X(j\omega)H(j\omega)$$, which means that the convolution in the time domain corresponds to the multiplication in the frequency domain.

- Example: Solving ODE
  Now lets use the multiplication in the frequency domain to compute the convolution of two signals.
  Consider two signals, $$x(t)=e^{-at}u(t)$$ and $$h(t)=e^{-bt}u(t)$$. Then, the Fourier transform of those signals are given by
  $$
  X(j\omega)= \frac{1}{a+j\omega},\;\; H(j\omega)=\frac{1}{b+j\omega}
  $$
  Therefore the frequency response, i.e. $$\mathcal{F}[y(t)]= Y(j\omega)$$ is computed by
  $$
  \begin{align*}
  Y(j\omega) &= X(j\omega)H(j\omega) \\&= \frac{1}{(b+j\omega)(a+j\omega)}\\
  &= \frac{1}{b-a}\bigg(\frac{1}{a+j\omega}-\frac{1}{b+j\omega}\bigg)
  \end{align*}
  $$
  By applying inverse Fourier transform (or duality), the time-domain response $$y(t)$$ is
  $$
  y(t)=\frac{1}{b-a}\big(e^{-at}u(t)-e^{-bt}u(t)\big)
  $$
  ## Low Pass Filter
  A low pass filter keeps the signals whose frequency is lower than the threshold, say $$w_c$$. THen, we can design a ideal low pass filter as
  $$
  H(j\omega) = \begin{cases}
  1 & \omega < \|\omega_c\|\\
  0 & \omega > \|\omega_c\|
  \end{cases}
  $$
  As it is a rectangular pulse in frequency domain, the impulse response in the time domain is a sinc function. By inverse Fourier transformation,
  $$
  h(t) = \frac{1}{2\pi}\int_{-\omega_c}^{\omega_c}e^{j\omega t}d\omega = \frac{\sin \omega_c t}{\pi t}
  $$
  However, since it is non-causal, it is hard to construct. Therefore, we use some approximate filter, such as
  $$
  e^{-at}u(t) \overset{F}{\leftrightarrow} \frac{1}{a+j\omega}
  $$
  Given filter emphasizes the low frequency signals, and diminishing amplitude for high frequency signals. As it is causal and non-oscillating, it is desirable.
