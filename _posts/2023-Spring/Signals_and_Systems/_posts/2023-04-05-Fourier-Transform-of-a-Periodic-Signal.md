---
layout: post
title: Fourier Series and Fourier Transform
tags: [Signals-and-Systems]
permalink: /2023-spring/signals-and-systems/fourier-series-and-transform
---

# Fourier Series와 Fourier Transform에 대한 이해

# Fourier Series

## Eigenfunction

$$s\in\mathbb{C}$$ 에 대하여 $$\phi(t)= e^{st}$$를 생각해보자. Impulse respones $$h(t)$$와 response $$y(t)$$에 대하여 다음 관계가 성립한다.

$$
\begin{align*}y(t) = h(t) * \phi(t) &= \int_{-\infty}^{\infty}h(\tau)\phi(t-\tau)d\tau\\&= e^{st}\int_{-\infty}^{\infty}h(\tau)e^{-s\tau}d\tau\\&= \phi(t) \int_{-\infty}^{\infty}h(\tau)e^{-s\tau}d\tau\\\end{align*}
$$

이 때, $$\int_{-\infty}^{\infty}h(\tau)e^{-s\tau}d\tau$$는 $$s$$에만 dependent하므로, 이를 $$H(s)$$로 나타낸다면 위의 수식은 다음과 같이 표기할 수 있다.

$$
y(t)=H(s)\phi(t)
$$

이 때, $$H(s)$$는 $$t$$에 대한 상수이므로, $$\phi(t)$$는 eigenfunction이며, $$H(s)$$는 이에 상응하는 eigenvalue이다.

## Periodic Signals

$$\phi(t)=e^{st}$$에서 우리는 $$s\in\mathbb{C}$$라고 가정을 하였다. 그런데 만약 $$s$$가 purely imaginary라면, 즉 $$\phi(t)=e^{j\omega_0 t}$$라면, Euler’s rule에 따라 다음과 같이 나타낼 수 있다.

$$
\phi(t) = e^{j\omega_0t}=\cos\omega_0t+j\sin\omega_0t
$$

따라서, eigenfunction $$\phi(t)$$는 frequency를 $$\omega_0$$으로하는 Sinusoidal signal이다.

그런데, Superposition에 의하여 우리는 임의의 input signal $$x(t)$$에 대하여 수많은 주기함수, $$\phi_k(t)=e^{-jk\omega_0t}$$의 Linear combination으로 표현할 수 있다. 즉,

$$
\begin{equation}x(t) = \sum_{k=-\infty}^{\infty}a_ke^{jk\omega_0t}
\end{equation}
$$

## Fourier Coefficients

앞서 임의의 input signal은 주기함수의 linear combination으로 표현 될 수 있음을 보였다. 그러나 Linear combination에서의 scaling factor, 즉 $$a_k$$ 를 구해야 완전하게 표현 할 수 있다.

먼저 $$(1)$$에서 양변에 $$e^{-jn\omega_0t}$$를 곱한다.

$$
x(t)e^{-jn\omega_0t}=\sum_{k=-\infty}^{\infty}a_ke^{-j(k-n)\omega_0t}
$$

그 다음, 양변을 길이가 $$T=2\pi/\omega_0$$인 임의의 구간에서 적분한다.

$$
\int_0^Tx(t)e^{-j(k-n)\omega_0t}dt=\sum_{k=-\infty}^{\infty}a_k\int_{0}^{T}e^{-j(k-n)\omega_0t}dt
$$

이 때 $$k\neq n$$이면, $$e^{-j(k-n)\omega_0t}$$는 주기가 $$\frac{1}{k-n}T$$ 인 Sinusoid이기 때문에, 길이가 $$T$$인 적분 구간에 대하여 적분하면 항상 $$0$$이된다. 따라서, $$\sum_k$$ $$a_k$$ 중에 $$k=n$$, 즉 $$a_n$$ 항을 제외하고는 모두 사라진다. 이를 다시 정리하면,

$$
\int_0^Tx(t)e^{-jn\omega_0t}dt = a_n\int_0^T1dt = a_nT
$$

따라서, 우리는 $$a_k$$를 다음과 같이 구할 수 있다.

$$
\begin{equation}
a_k =\frac{1}{T}\int_0^Tx(t)e^{-jk\omega_0t}dt
\end{equation}
$$

이 때의 $$a_k$$를 Fourier Coefficient라고 한다.

## Dirichlet Condition

그러나, 사실 모든 주기함수에 대하여 Fourier Series가 존재하는 것은 아니다. Infinite Fourier Series가 존재하기 위한 조건을 Direichlet condition이라 하며, 이는 다음과 같다.

1. 임의의 한 주기에 대하여 Absolutely Integrable이다. 즉, $$\int_T \|x(t)\|dt <\infty$$.
2. 임의의 구간에 대하여 유한한 극대, 극소가 있어야한다. $$\sin(1/t)$$와 같이 $$0$$으로 수렴할 때 무한히 진동하는 signal은 이를 위배한다.
3. 임의의 구간에 대하여 유한한 점에서 불연속이여야한다.

이 중 1번 조건은 이후 Fourier Transform에서 다시 주목할 것이다.

## Properties

- Linearity: $$\alpha x(t) +\beta y(t) \rightarrow \alpha a_k + \beta b_k$$
- Time shifting: $$x(t-t_0)\rightarrow e^{-jk\omega_0t_0}a_k$$
- Time reversal: $$x(-t) \rightarrow a_{-k}$$
- Conjugation: $$\overline{x(t)}=\overline{a_{-k}}$$
- Multiplication: $$c_n = \sum_{k=-N}^{N}a_kb_{n-k}$$

# Fourier Transform

## Rerpresentaion of Apreiodic Signals

앞서 Fourier series는 periodic signal에 주목했다. 하지만 unit step, impulse와 같이 aperidic signal 또한 우리는 이와 비슷한 형태로 나타내고자 한다. 우선, $$x(t)$$를 $$(-T/2, T/2)$$에서 1인 signal, $$\tilde{x}(t)$$는 $$x(t)$$를 반복하는 periodic signal이라고 하자. 그러면 periodic signal $$\tilde{x}$$에 대하여 다음과 같이 나타낼 수 있다 ($$w_0 = 2\pi/T)$$

$$
\begin{equation}\tilde{x}(t) = \sum_{k=-\infty}^{\infty}a_ke^{jk\omega_0t}
\end{equation}
$$

$$
\begin{equation}
a_k =\frac{1}{T}\int_{-T/2}^{T/2}\tilde{x}(t)e^{-jk\omega_0t}dt\end{equation}
$$

그런데, $$x(t)$$는 $$(-T/2, T/2)$$ 이외의 구간에서 $$0$$으로 정의되어있으므로, $$(4)$$을 다음과 같이 표현할 수 있다.

$$
a_k=\frac{1}{T}\int_{-\infty}^{\infty}x(t)e^{-jk\omega_0t}dt
$$

따라서, $$X(j\omega)$$를 다음과 같이 정의하면,

$$
X(j\omega)=\int_{-\infty}^{\infty}x(t)e^{-jk\omega_0t}dt
$$

$$a_k$$는 다음과 같이 표현할 수 있다.

$$
\begin{equation}
a_k= \frac{1}{T}X(j\omega)=\frac{\omega_0}{2\pi}X(j\omega)
\end{equation}
$$

그렇다면, $$x(t)$$를 이용해 만든 periodic signal인 $$\tilde{x}(t)$$는 $$(3)$$과 $$(4)$$에 의하여 다음과 같이 표현된다.

$$
\begin{equation} \tilde{x}(t) = \sum_{k=-\infty}^{\infty}\frac{1}{T}X(j\omega)e^{jk\omega_0t} = \frac{1}{2\pi}\sum_{k=-\infty}^{\infty}X(j\omega)e^{-jk\omega_0t}\omega_0
\end{equation}
$$

그런데, $$T\rightarrow \infty$$ 를 가정해보자. 그렇다면 $$\tilde{x}\rightarrow x(t)$$이고, $$\omega_0=2\pi/T\rightarrow 0$$ 이다. 즉, 우리는 aperiodic signal을 주기가 무한한 periodic signal로 이해하는 것이다. 따라서 $$T\rightarrow \infty$$ 에 따라, 합으로 표현된 $$(6)$$을 $$(7)$$과 같이 Integral으로 표현할 수 있다.

$$
\begin{equation}x(t)= \frac{1}{2\pi}\int_{\infty}^{\infty}X(j\omega)e^{j\omega t}d\omega
\end{equation}
$$

또한, 반대로,

$$
\begin{equation}
X(j\omega)=\int_{-\infty}^{\infty}x(t)e^{-j\omega t}dt\end{equation}
$$

이를 $$(8)$$을 Fourier Transform이라고 하며, 이를 통해 aperiodic signal 또한 periodic signal에 적용했던 것과 유사한 방법을 사용할 수 있다.

## Fourier Transform of Periodic Signals

이제 Fourier transform에 대한 논의를 aperiodic signal에서 periodic signal로 연장한다. 우선 주기함수 $$x(t)$$와 그의 Fourier transform pair $$X(j\omega)$$가 있고, $$X(j\omega)$$가 다음과 같다고 하자.

$$
\begin{equation}X(j\omega)= 2\pi\delta(\omega-\omega_0)
\end{equation}
$$

$$\int_{-\infty}^{\infty}\delta(t)dt=1$$이므로, $$X(j\omega)$$는 넓이가 $$2\pi$$이고, $$\omega = \omega_0$$에서의 impulse라고 이해할 수 있다. 따라서, inverse Fourier transform에 의해 $$x(t)$$는 다음과 같이 구할 수 있다.

$$
x(t)=\frac{1}{2\pi}\int_{-\infty}^{\infty}2\pi\delta(\omega-\omega_0)e^{j\omega t}d\omega
$$

이때, $$\delta(\omega-\omega_0)$$은 $$\omega = \omega_0$$일 때만 $$1$$이므로, $$x(t)$$는 다음과 같이 간단히 할 수 있다.

$$
x(t)=e^{j\omega_0t}
$$

Fourier series에서 논의하였듯이, $$e^{j\omega_0t}$$는 $$\omega_0$$을 주기로하는 sinusoid이다. 따라서, $$(9)$$와 같은 형태의 inverse Fourier transform은 periodic signal이다. 다시 말하자면, time-domain에서의 periodic signal은 frequency domain에서의 impulse function으로 나타내어진다.

더 일반적으로,

$$
\begin{equation}X(j\omega)= \sum_{k}2\pi a_k \delta(\omega-k\omega_0)
\end{equation}
$$

에 대하여, periodic signal $$x(t)$$는 Fourier series와 같이 나타내어진다.

$$
\begin{equation}x(t)=\sum_{k=-\infty}^{\infty}a_ke^{jk\omega_0t} \end{equation}
$$

$$(10)$$과 같이 impulse function이 일정한 간격(equispace)로 주어진 signal을 impulse train 또는 Dirac comb이라고 한다.

예를 들어 $$\cos(\omega_0t)$$를 Fourier transform을 이용해 나타내고자 한다하자.

$$
\cos(\omega_0t) =\frac{e^{j\omega_0t}+e^{-j\omega_0t}}{2}
$$

이므로, Fourier coefficient가 $$a_1 = \frac{1}{2}$$, $$a_{-1}=\frac{1}{2}$$임을 간단히 알 수 있다. Fourier transform으로 같은 결과가 도출되는지 확인해보자.

$$
\begin{align*}X(j\omega)&= \int_{-\infty}^{\infty}\frac{e^{-j(\omega-\omega_0)t} + e^{-j(\omega+\omega_0)t}}{2}dt \\
&= 2\pi\times \frac{1}{2}(\delta(\omega-\omega_0) + 2\pi \delta(\omega+\omega_0))\\
\end{align*}
$$

여기에서도 $$2\pi a_1 = \pi \rightarrow a_1 = \frac{1}{2}$$, $$a_{-1}=\frac{1}{2}$$임을 확인할 수 있다.

사실 $$e^{j\omega_0t}$$의 Fourier transform이 왜 $$2\pi\delta(\omega-\omega_0)$$이 되는지는 직관적으로 잘 와닿지 않는다. $$(-\infty, \infty)$$이면 주기를 무한히 반복해서 sinusoid의 적분값이 0이 될테니 $$\omega \neq \omega_0$$일때는 항상 $$0$$인 것까지는 이해하기 쉬우나, $$\omega = \omega_0$$일 때 그 적분값이 왜 $$2\pi$$가 나오는지는 확실히 이해하지 못했다.

우선은 $$(9)$$에서의 가정을 통해 inverse Fourier transform을 이끌어내는 것이 더 확실할 것 같다.

## Properties

- Linearity : 당연하다. Integral이 linear operator이기 때문이다.
- Time Shifting:

$$
\mathcal{F}[x(t-t_0)]= e^{-j\omega t_0}X(j\omega)
$$

- Time and Period scaling:

$$
\mathcal{F}[x(at)]= \frac{\|a\|}X(\frac{j\omega}a)
$$

- Differentiation:

$$
\mathcal{F}\bigg[\frac{dx(t)}{dt} \bigg]=j\omega X(j\omega)
$$

- Integration:

  $$
  \mathcal{F}\bigg[\int_{-\infty}^tx(\tau)d\tau\bigg]= \frac{1}{j\omega}X(j\omega)+\pi X(0)\delta(\omega)
  $$

  - 마지막 $$\pi X(0)\delta(\omega)$$는 평균 에너지의 직류로 이해할 수 있다. 자세한 유도는 다음과 같다.
    $$
    \begin{align*}
    \int_{-\infty}^{t}x(\tau)d\tau &= \int_{-\infty}^{\infty}x(\tau)u(t-\tau)d\tau \\
    &= X(j\omega)U(j\omega)\\
    &= X(j\omega)(\frac{1}{j\omega}+\pi\delta(\omega))\\
    &= \frac{X(j\omega)}{j\omega}+\pi X(0)\delta(\omega)
    \end{align*}
    $$
  - 이때, $$U(j\omega)$$는 다음과 같이 구할 수 있다.

    $$
    u'(t) = \delta(t)\\
    j\omega U(j\omega) = \mathcal{F}[u(t)'] = 1\\
    U(j\omega ) = \frac{1}{j\omega} + c\delta(\omega)\\
    $$

    $$u(0)=\frac{1}{2}$$으로 정의할 수 있으므로 (계단함수의 정의는 필요에 따라 바뀔 수 있다.)

    $$
    \begin{align*}u(0) &=\frac{1}{2\pi}\int_{-\infty}^{\infty}U(j\omega)e^{j\omega t}d\omega \\
    &= \frac{1}{2\pi} \int_{-\infty}^{\infty}c\delta(\omega)d\omega \\
    &=\frac{1}{2\pi}c = \frac{1}{2}
    \end{align*}
    $$

    따라서, $$c = \pi$$이므로, $$U(j\omega) = \frac{1}{j\omega}+\pi\delta(\omega)$$이다.
    또는 signum 함수를 이용하여 계산할 수 있다.

    $$
    \text{sgn}(x) = \begin{cases} 1 & x > 0\\
    0 & x = 0 \\
    -1 & x < 0
    \end{cases}
    $$

    $$u(t)$$를 signum 함수를 이용하여 나타내면 다음과 같다.

    $$
    u(t)= \frac{1}{2}(1+\text{sgn}(t))
    $$

    이는 앞서 이용한 계단함수의 정의와 같다. $$(u(0)=0.5)$$
    그리고, signum 함수는 극한을 이용해 다음과 같이 나타낼 수 있다.

    $$
    \text{sgn}(t) = \lim_{a\rightarrow0} [e^{-at}u(t)-e^{at}u(-t)]
    $$

    이를 이용해서 $$U(j\omega)$$를 계산해보자.

    $$
    \begin{align*}
    U(j\omega)&= \int_{-\infty}^{\infty}\frac{1}{2}\big[1+ \lim_{a\rightarrow 0}[e^{-at}u(t)-e^{at}u(-t)]\big]e^{-j\omega t}dt\\
    &= \frac{1}{2}\times 2\pi\delta(\omega)+ \frac{1}{2}\lim_{a\rightarrow0}\big[\int_0^\infty e^{-a-j\omega t}dt -\int_{-\infty}^0e^{a-j\omega t}dt \big]\\
    &=\pi\delta(\omega)+\frac{1}{2}\lim_{a\rightarrow0} [\frac{1}{a+j\omega}-\frac{1}{a-j\omega}]\\
    &=\pi\delta(\omega)+\frac{1}{2}\times \frac{2}{j\omega}\\
    &= \frac{1}{j\omega}+\pi\delta(\omega)
    \end{align*}
    $$

- Duality: A의 Fourier transform이 B라고 하자. 그렇다면 B의 Fourier Transform도 A이다. (inverse Fourier Transform이 아니다) 예를 들어 rectangle pulse의 Fourier Transfrom은 sinc function이며, sincfunction의 Fourier transform 또한 rectangle pulse이다.

$$
1 \overset{F}{\leftrightarrow} \delta(\omega)\\
e^{j\omega_0t} \overset{F}{\leftrightarrow} \delta(\omega - \omega_0) \\
\text{rect} \overset{F}{\leftrightarrow} \text{sinc}
$$

## Convolution

Time-domain에서의 convolution은 다음과 같이 주어진다.

$$
x(t)* h(t) = \int_{-\infty}^{\infty}x(\tau)h(t-\tau)d\tau
$$

이 convolution의 Fourier transform을 구해보면,

$$
\begin{align*}
x(t)*h(t) &=\int_{-\infty}^{\infty}\int_{-\infty}^{\infty}x(\tau)h(t-\tau)d\tau e^{-j\omega t} dt\\
&=\int_{-\infty}^{\infty}x(\tau)\int_{-\infty}^{\infty}h(t-\tau)e^{-j\omega t}dt d\tau \\
&= \int_{-\infty}^{\infty}x(\tau)\int_{-\infty}^{\infty}h(t-\tau)e^{-j\omega(t-\tau)}dt e^{-j\omega \tau}d\tau\\
&= \int_{-\infty}^{\infty}x(\tau)e^{-j\omega \tau}H(j\omega)d\tau\\
&= X(j\omega)H(j\omega)

\end{align*}
$$

따라서, Time-domain에서의 convolution은 frequency-domain에서의 mulitplication으로 이해할 수 있다.
