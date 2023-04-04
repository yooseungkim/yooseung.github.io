---
layout: post
title: Linear Regression (i)
tags: [MLDL]
permalink: /2023-spring/mldl/linear-regression-1
---

# Linear Regression (i)

# Linear Model

## Simple Linear Model

A simple linear model is given by

$$
Y = mX +b
$$

where $$Y$$ is response variable, $$X$$ is covariate, $$m$$ is a slope and $$b$$ is an intercept (bias). It can be also represented as

$$
y=\theta^T\vec{x}+\epsilon + b
$$

A $$\theta$$ is a vector of parameters, therefore $$\theta^T\vec{x}$$ is the linear combination of covariates.

$$
\begin{bmatrix}
\theta_1\\
\vdots\\
\theta_p
\end{bmatrix} \cdot[x_1 \cdots x_p] = \sum_{i=1}^{p}\theta_ix_i
$$

An $$\epsilon$$ is a real value noise that follows normal distribuition, i.e., $$\epsilon \sim N(0,\sigma^2)$$
Also, if we define $$x_{p+1}= 1$$, then we have

$$
y= \begin{bmatrix}
\theta_1\\
\vdots\\
\theta_p\\
b
\end{bmatrix} \cdot [x_1,\cdots, x_p , 1] + \epsilon = \theta^T\vec{x}+\epsilon+b
$$

Therefore, $$b$$ can be considered as a parameter of $$x_{p+1} := 1$$. For notational simplicity, we will redefine $$p := p+1$$.

## Linear Regression

What we want to learn by linear regression is a mapping $$f$$, from $$x_i$$ to $$y_i$$.
Let denote the set of basis functions $$H=\{h_1, \cdots, h_K\}$$. Then, we can say that

$$
y_i \approx \hat{y_i} = \hat{f}(x_i) = \sum_kw_kh_k(x_i)
$$

Then we will find the coefficients (parameters) $$w_k$$ such that minimze the total error,

$$
Total\ Error = \sum_i (y_i-\hat{y_i})^2 = \sum_i\bigg(y_i-\sum_kw_kh_k(x_i)\bigg)^2
$$

It is called **linear regression** because the model is linear in parameters, not in covariate $$x$$. Although if $$h_k(x_i) = x^2_i$$, it is still linear in parameters, so it is also a linear regression.

Therefore, it can be also used for $$Y$$ with non-linear responses.

## Feature Space

Our feature $$x_i$$ is of the form

$$
x_i=(X_{i,1}, X_{i,2},\dots, X_{i,p}) \in \mathbb{R}^p
$$

Then apply non-linear transform $$\phi: \mathbb{R}^p \rightarrow \mathbb{R}^k$$, we have, for example,

$$
\phi(x) =\{1, x, x^2, \dots, x^{k-1}\}
$$

The element of $$\phi(x)$$ is $$h_k(x)$$, which can be

- Lines: $$y=ax+b+\epsilon$$
- Polynomials: $$y=ax^2+bx+c + \epsilon$$
- others: $$y=a\sin(x)+b+\epsilon$$

# Solving Linear Regression

The final goal of linear regression is minimizing the sum of residual or squared error. Formally, finding $$\mathbf{w}^*$$ such that

$$
\begin{equation}\mathbf{w}^* = \arg\min_\mathbf{w} \sum_{j=1}^N\bigg(t(\mathbf{x_j})-\sum_{i=1}^{k}w_ih_i(\mathbf{x_i})\bigg)^2
\end{equation}
$$

## Matrix Representation

Now we will rewrite our expression with the matrix notation. First, represent data as

$$
\mathcal{D} = \{(x_i, y_i)\}_{i=1}^n,\;\; x_i\in \mathbb{R}^p
$$

Then, the covariate matrix $$X$$ $$\in M_{n\times p}$$ and the response vector $$Y \in \mathbb{R}^n$$ are of the form

$$
X= \begin{bmatrix}
x_{11}&\cdots& x_{1p}\\
&\vdots&\\
x_{n1}&\cdots &x_{np}
\end{bmatrix} \text{ and } Y=\begin{bmatrix}
y_1\\
\vdots\\
y_n
\end{bmatrix}
$$

We will assume $$X$$ is invertible, that is, $$rank(X)=p$$.

Then, the equation $$Y=X\theta+\epsilon$$ can be visualized as following

![Shape of each components ](<Linear%20Regression%20(i)%202c3033338c1d4f0aa82ae2a19f0bca3a/Untitled.png>)

Shape of each components

Now let’s get back to linear regression expressed as $$(1)$$. Let denote $$y=t(x)$$. Then,
$$H = \{h_1,\dots, h_K\},  \mathbf{w} = \{w_1,\dots, w_K\}, \mathbf{t} = \{t_1, t_2, \dots, t_N\}$$ are the form of

$$
H=\begin{bmatrix}
\| & &\|\\
h_1&\cdots & h_K\\
\|& & \|
\end{bmatrix}, \; \mathbf{w}=\begin{bmatrix}
w_1\\
\vdots\\
w_K
\end{bmatrix},\;
\mathbf{t} = \begin{bmatrix}
t_1\\
\vdots\\
t_N
\end{bmatrix}
$$

Therefore, $$\sum_iw_ih_i(\mathbf{x}_j)$$ represents the inner product of $$\mathbf{w}$$ and $$j$$-th row of $$H$$. Moreover,

$$
\sum_{j=1}^N\bigg(t(\mathbf{x_j})-\sum_{i=1}^{k}w_ih_i(\mathbf{x_j})\bigg)^2= (H\mathbf{w}-\mathbf{t})^T(H\mathbf{w}-\mathbf{t})
$$

Thus, $$(1)$$ can be rewritten as

$$
\begin{equation}\mathbf{w}^*=\argmin_\mathbf{w} (H\mathbf{w}-\mathbf{t})^T(H\mathbf{w}-\mathbf{t})
\end{equation}
$$

A solution of $$(2)$$ is given by

$$
\mathbf{w}^* = \big(H^TH\big)^{-1}H^Tt
$$

- Specific Derivation
  ![Untitled](<Linear%20Regression%20(i)%202c3033338c1d4f0aa82ae2a19f0bca3a/Untitled%201.png>)

We will denote $$A =H^TH$$ and $$\mathbf{b} = H^{-1}t$$ . Then the solution is given by

$$
\mathbf{w}^* = \mathbf{A}^{-1}\mathbf{b}
$$

Note that $$A$$ and $$\mathbf{b}$$ are the form as following:

![Untitled](<Linear%20Regression%20(i)%202c3033338c1d4f0aa82ae2a19f0bca3a/Untitled%202.png>)

## Sum Squared Error

Why do we use sum squared error? As we assume error be Gaussian (Gaussian noise),

$$
\mathbf{t}(\mathbf{x}) = \sum_iw_ih_i(\mathbf{x})+\epsilon = N(\mathbf{w}^Th(\mathbf{x}), \sigma^2)
$$

Then, the probability of $$t$$ under $$\mathbf{x}, \mathbf{w}, \sigma$$ is given by

$$
P(t\|\mathbf{x},\mathbf{w},\sigma)=\frac{1}{\sigma\sqrt{2\pi}}e^{\frac{-[t-\sum_iw_ih_i(\mathbf{x})]^2}{2\sigma^2}} \;\; \text{(Gaussian)}
$$

Now, from given data, we will estimate $$\mathbf{w}$$ with MLE. First, we will derive the $$\log$$-likelihood and find $$\mathbf{w}_{ML}$$ such that maximizes the $$\log$$-likelihood.
