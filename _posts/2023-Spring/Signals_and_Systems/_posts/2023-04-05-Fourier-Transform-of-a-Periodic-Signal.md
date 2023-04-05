---
layout: post
title: Fourier Transform of a Periodic Signal
tags: [Signals-and-Systems]
permalink: /2023-spring/signals-and-systems/fourier-transform-of-periodic-signal
---

# Fourier Transform of a Periodic Signal

## Fourier Series

### Eigen Function

$$s\in \mathbb{C}$$ 에 대하여 $$\phi(t) = e^{st}$$을 생각해보자. Impulse Response $$h(t)$$와 Response $$y(t)$$에 대하여 다음 관계가 성립한다.

$$
\begin{align*}
y(t) = h(t) * \phi(t) &= \int_{-\infty}^{\infty}h(\tau)\phi(t-\tau)d\tau\\
&= e^{st}\int_{-\infty}^{\infty}h(\tau)e^{-s\tau}d\tau\\
&= \phi(t) \int_{-\infty}^{\infty}h(\tau)e^{-s\tau}d\tau\\
\end{align*}
$$

이 때, $$\int_{-\infty}^{\infty}h(\tau)e^{-s\tau}d\tau\\$$는 $s$에 대해 변수이지만, $\tau$에 대해 상수이므로 이를 $H(s)$로 나타낸다면 위는 다음과 같이 표현 할 수 있다.

$$
y(t) = H(s)\phi(t)
$$

따라서, $\phi(t)$는 Eigenfunction이며, H(s)는 이에 상응하는 Eigenvalue이다.

### Periodic Signals

$\phi(t) = e^{st}$에서 우리는 $s$가 Complex number이라고 가정을 했다. 그런데 만약 s가 purely imaginary라면, 즉, $\phi(t)=e^{j\omega_0 t}$라면, Euler's rule에 따라 다음과 같이 표현 할 수 있다.

$$
\phi(t)=e^{j\omega_0 t} = \cos(\omega_0t) + j\sin(\omega_0t)
$$

따라서, $s=j\omega_0$라면, eigenfunction $\phi(t)$는 frequency를 $\omega_0$으로 하는 Sinusoidal Signal이다.

Superposition property에 의하여, 임의의 input signal은 수많은 주기함수의 linear combination으로 이해될 수 있다.

## Fourier Transform

기본적으로, 푸리에 변환과 그 역변환은 다음과 같이 정의된다.

$$
X(j\omega) = \int_{-\infty}^{\infty} x(t) e^{-j\omega t}dt \\
x(t) = \frac{2}{\pi}
\int_{-\infty}^{\infty} X(j\omega) e^{j\omega t}d\omega
$$
