---
layout: post
title: Bias-Variacne Tradeoff
tags: [MLDL]
permalink: /2023-spring/mldl/bias-variance
---

# Bias-Variance Tradeoff

# Bias and Variance

## Bias

For each given dataset $$D$$ with $$m$$ samples, the learner will learn different functions $$h(x)$$. The expected prediction $$E_D[h(x)]$$ can be obtained by computing the average of different functions that have learned.

The **bias** is the difference between the expectation perdiction $$E_D[h(x)]$$ and truth $$t(x)$$. It measures how much it is close to the true solution. It decreases with complex models.

The squared bias is computed by

$$
bias^2 = \int_x \big(E_D[h(x)-t(x)]\big)^2 p(x) dx \\
= \mathbb{E}\bigg[(\mathbb{E}_D[h(x)]-t(x))^2\bigg]
$$

It can be understood as the **\***expected difference**\*** between \***\*\*\*\*\***expected prediction\***\*\*\*\*\*** and **\*\***truth.**\*\***

## Variance

The variance is the difference between what you expect to learn and what you learned from a particular dataset. Therefore, it measures how much sensetive the learner is to the specific dataset. It decreases for the simple model, since simple models do not stick to the specific dataset.

$$
variance= \int E_D\big[(h(x)-\bar{h}(x))^2\big]p(x)dx\\
= \mathbb{E}\bigg[\mathbb{E}\big[\big(h(x)-\bar{h}(x)\big)^2\big]\bigg]
$$

where $$\bar{h}(x) = E_D[h(x)]$$. As $$h(x)$$ is what you actually learned, $$h(x)-\bar{h}(x)$$ is the differnce between the expected learn and the acutal learn.

# Bias-Variance Decomposition

Consider a regression problem,

$$
t = f(x) = g(x) + \epsilon
$$

where $$t$$ is the true value and $$g(x)$$ is the true model and $$\epsilon \sim N(0, \sigma^2)$$ is the noise. After learning, we will obtain a function $$h(x)$$, such that $$h(x) \sim g(x)$$.

The true risk of the function $$h(x)$$ is given by

$$
R(h) = E[E_D[L(h(x), t)]]\\
= E_D\bigg[\int_x\int_t (h(x)-t)^2 p(t\|x)p(x)dtdx\bigg]
$$

## Noise

Although we have perfect learner and infinite data, there remains an unavoidable error $$\sigma^2$$, due to the noise $$\epsilon \sim N(0, \sigma^2)$$. As we assumed the perfect learner, $$h(x)  = g(x)$$. Therefore,

$$
(h(x)-t)^2 = (h(x)-g(x)-\epsilon)^2  = \sigma^2
$$

## Bias-Variance Decomposition of Error

Let $$y_n = f(\mathbf{x}_n;\theta) + \epsilon$$, where $$\epsilon \sim N(0, \text{Var}(\epsilon))$$. And let the function $$\hat{f}$$ denote the learned function. Then, $$\mathbb{E}[\hat{f}]$$ is the expected learned function and $$f$$ is the true value.

Now, comptue the error between the true value with noise $$y$$ and the learned function $$\hat{f}$$.

Then, we have

$$
 \mathbb{E}\bigg[\big(y-\hat{f}\big)^2\bigg]=\text{Var}(\epsilon)+\mathbb{E}\bigg[\big(\hat{f}-\mathbb{E}[\hat{f}]\big)^2\bigg] + \big(\mathbb{E}[\hat{f}]-f\big)^2
$$

Each term on the right hand side represents unavoidable error $$\sigma^2$$, $$variance$$ and $$bias^2$$, respectively.

## True Risk

The true risk is the expected risk (or test risk). Similarly, it can be decomposed to

$$
\begin{align*}
R(h) &= \mathbb{E}[(h(X)-t)^2]\\
&= \mathbb{E}[(h(X)-\mathbb{E}[h(X)])^2]\;\; (variance)\\
&+ \mathbb{E}[(\mathbb{E}[h(X)]-g(X))^2]\;\;\ (bias^2)\\
&+ \sigma^2 \;\;\; (Bayes\ error)
\end{align*}
$$

## Bias-Variance Tradeoff

A model with more complex class tends to have less bias but high variance.

A model with less complex class tends to have high bias but low variance.

# Error

## Training Error (Empirical Error)

For a given dataset, **training error** is the loss function on the training data for a particular set of parameter $$\mathbf{w}$$.

$$
error_{train}(\mathbf{w}) =\frac{1}{N}\sum_{j=1}^N\bigg(t(\mathbf{x_j})-\sum_i w_ih_i(\mathbf{x}_j)\bigg)^2
$$

where $$N$$ is the number of data points in the training data.

Training error will decrease if the model gets more complex. However, training error is the poor measure of the quality of solution. Therefore, we need to introduce new measure of the quality of solution.

## Prediction Error (True Error)

Unlikely to the training error, it cares the error over all possibilities, not limited to the training set.

$$
error_{true}(\mathbf{w})= \int_\mathbf{x}\bigg(t(\mathbf{x}_j)-\sum_i w_ih_i(\mathbf{x}_j)\bigg)^2p(\mathbf{x})d\mathbf{x}
$$

![Untitled](Bias-Variance%20Tradeoff%205d4234e59ed64f9d97ff2df736893a38/Untitled.png)

The graph above shows the relationship between training error and prediction error. As it can be seen in the figure, the difference between true risk and empirical risk increases as the model gets more complex. Therefore, training error is not a good measure.

## Sampling the True Error

However, the true error is hard to compute, since we do not know $$t(\mathbf{x})$$ for every $$\mathbf{x}$$ and do not know the exact probability $$p(\mathbf{x})$$.

Thus, we will approximate the integral to sum by sampling, by assuming a set of i.i.d points $$\{x_1,\dots, x_M\}$$ from $$p(x)$$.

$$
error_{true}(\mathbf{x}) \approx \frac{1}{M}\sum_{j=1}^M \bigg(t(\mathbf{x}_j)-\sum_i w_ih_i(\mathbf{x}_j)\bigg)^2
$$

For a given dataset, we will split it into two parts of training data and test data. Then, find the opimal parameter $$\mathbf{w}$$ for the training data and evaluate the true error with

$$
error_{test}(\mathbf{x}) \approx \frac{1}{N_{test}}\sum_{j=1}^{N_{test}}\bigg(t(\mathbf{x}_j)-\sum_i w_ih_i(\mathbf{x}_j)\bigg)^2
$$

## Overfitting

![Untitled](Bias-Variance%20Tradeoff%205d4234e59ed64f9d97ff2df736893a38/Untitled%201.png)

Simply, $$h$$ overfits the training data if it has low training error but high test error. Formally, $$h$$ overfits the training data if $$\exists h'$$ such that

$$
error_{train}(h) < error_{train}(h')\\
error_{test}(h) > error_{test}(h')
$$

## Summary

The ground (GND) truth is ideal error, assuming we know $$t(x)$$ and $$p(x)$$ for all $$x$$.

$$
error_{true}(\mathbf{w})= \int_\mathbf{x}\bigg(t(\mathbf{x}_j)-\sum_i w_ih_i(\mathbf{x}_j)\bigg)^2p(\mathbf{x})d\mathbf{x}
$$

The training error is optimistically biased toward $$\mathbf{w}$$, since the model is optimized to the $$\mathbf{w}$$, so that trainig error becomes low.

$$
error_{train}(\mathbf{w}) =\frac{1}{N}\sum_{j=1}^N\bigg(t(\mathbf{x_j})-\sum_i w_ih_i(\mathbf{x}_j)\bigg)^2
$$

The test error is our final measure, obtained by sampling the true error with test set.

$$
error_{test}(\mathbf{x}) \approx \frac{1}{N_{test}}\sum_{j=1}^{N_{test}}\bigg(t(\mathbf{x}_j)-\sum_i w_ih_i(\mathbf{x}_j)\bigg)^2
$$
