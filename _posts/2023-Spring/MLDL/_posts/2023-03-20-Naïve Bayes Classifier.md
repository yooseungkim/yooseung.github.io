---
layout: post
title: Naive Bayes Classifier (i)
tags: [MLDL]
permalink: /2023-spring/mldl/naive-bayes-1
---

# Naïve Bayes Classifier

# Classifier

## Supervised Learning

For given labeled training set $$\{(x_i, y_i)\|i =1,\dots,n\}$$, find a approximation to $$f:X\rightarrow Y$$, which is called **hypothesis.**

## Classification

A classification task predict a label(classes) $$y$$ for inputs $$x$$. A decision tree is one example of the classifier.

We want to directly estimate the data distribution $$P(X,Y)$$ . Then we would need prior $$P(Y)$$ and the likelihood $$P(X\|Y)$$. However, if $$X$$ consists of $$n$$ binary features, we have $$2^n-1$$ possibilities. This makes too complex model, which may have high variance. Therefore, we apply inductive bias to make the model simpler.

# Independence

## Independence

Two random variables $$X$$ and $$Y$$ are said to be **independent** if

$$
P(X,Y) = P(X)P(Y)\\
P(X\|Y)=P(X)
$$

If $$X$$ and $$Y$$ are independent, they don’t contain information about each other. In other words, observing $$Y$$ does not help predicting $$X$$ and vice versa. For example, winning on roulette this week does not help us predict the roulette next week.

## Conditional Independence

Formally, $$X$$ is **conditionally independent** of $$Y$$ given $$Z$$,

$$
P(X,Y\|Z)=P(X\|Z)P(Y\|Z)
$$

This implies that knowing $$Z$$ makes $$X$$ and $$Y$$ independent. Also,

$$
\begin{align*}P(X,Y\|Z) &=\frac{P(X,Y,Z)}{P(Z)}\\&= \frac{P(X,Y,Z)}{P(Y,Z)}\frac{P(Y,Z)}{P(Z)} \\&=P(X\|Y,Z)P(Y\|Z)\\

&= P(X\|Z)P(Y\|Z)\\
\end{align*}
$$

Therefore, we get an equation,

$$
\begin{equation}
\therefore P(X\|Y,Z)=P(X\|Z)
\end{equation}
$$

$$(1)$$ says that given $$Z$$, knowing $$Y$$ does not give more information about $$X$$ (conditional independence). However, it does not mean that $$X$$ and $$Y$$ are completely independent.

- **Exercise**
  ![Untitled](Nai%CC%88ve%20Bayes%20Classifier%200c186b8e0b6d4fee9731c881bacd1035/Untitled.png)
  - Is $$smart$$ independent of $$study$$?
    - $$P(smart, study) = 0.432 + 0.048 = \boxed{0.48}$$
    - $$P(smart)=0.48 + 0.32 = 0.8$$
    - $$P(study)=0.48+0.12= 0.6$$
    - $$P(smart)P(study)=\boxed{0.48}$$
    - Therefore, $$smart$$ and $$study$$ are independent
  - Is $$prepared$$ independent of $$study$$?
    - $$P(prepared, study) = 0.432+0.084=0.516$$
    - $$P(prepared)=0.516+0.168=0.684$$
    - $$P(study)=0.6$$
    - $$P(prepared)P(study)=0.6\times 0.684=\boxed{0.410}$$
    - Therefore, $$prepared$$ and $$study$$ are dependent.
  ![Untitled](Nai%CC%88ve%20Bayes%20Classifier%200c186b8e0b6d4fee9731c881bacd1035/Untitled%201.png)
  - Is $$smart$$ conditionally independent of $$prepared$$, given $$study$$?
    - $$P(smart, prepared\|study) = \frac{0.405}{0.70} = 0.579$$
    - $$P(smart\|study)=\frac{0.45}{0.70}=0.643$$
    - $$P(prepared\|study)=\frac{0.53}{0.70}=0.757$$
    - $$P(smart\|study)P(prepared\|study)=\boxed{0.487}$$
    - Therefore, $$smart$$ is not conditionally independent of $$prepared$$, given $$study$$
  - Is $$study$$ conditionally independent of $$prepared$$, given $$smart$$?
    - $$P(study, prepared\|smart)=\frac{0.405}{0.5}=\boxed{0.81}$$
    - $$P(study\|smart)=\frac{0.45}{0.5}=0.9$$
    - $$P(prepared\|smart)=\frac{0.45}{0.5}=0.9$$
    - $$P(study\|smart)P(prepared\|smart)=\boxed{0.81}$$
    - Therefore, $$study$$ is conditionally independent of $$prepared$$, given $$smart$$
    - That is, if we know the students are smart, knowing they studied do not help us predict whether they are prepared or not.

# Naïve Bayes Model

## Naive Bayes Assumption

In the Naive Bayes model, we assume that features are conditionally independent given class. That is, given class, each feature gives no more information about each other. In general,

$$
P(X_1, X_2,\dots,X_n\|Y)=\prod_iP(X_i\|Y)
$$

If $$X$$ has $$n$$ binary features and $$Y$$ has $$k$$ classes, we need $$O(kn)$$ parameters if we assume conditional independence between features. (each of $$k$$ classes has $$n$$ likelihood $$P(X_i\|Y)$$) However, without conditional independent assumption, we need $$O(k(2^n-1))$$ parameters. Therefore, assuming conditional independence reduces the parameters a lot.

## Naive Bayes Classifier

We have some information to classify the data

- Prior $$P(Y)$$
- $$n$$ conditionally independent features $$X$$ given the class $$Y$$
- Likelihood $$P(X_i\|Y)$$ for each $$X_i$$

Our logic is the same as before, we will classify a data into class $$y\in Y$$ such that maximizes the posterior. In other words, we pick the most probable $$y$$. As we know both prior and likelihood, we will use MAP instead of MLE.

Here is our decision rule for Naive Bayes Classifier

$$
\begin{align*}
y^*= h_{NB}(x) &= \arg\max_yP(Y =y)P(x_1, x_2, \dots,x_n\|y)\\
&=\arg\max_yP(y)P(x_1\|y)\cdots P(x_n\|y)\cdots\text{(conditional independence)}\\
&=\arg\max_yP(y)\prod_iP(x_i\|y)
\end{align*}
$$

It is known that if certain assumption holds, Naive Bayes classifier is an optimal classifier.

## Naive Bayes for Digits

First simplify the problem by assuming

- One feature $$F_{ij}$$ for each grid position $$(i,j)$$
- Possible features are $$0$$ or $$1$$
- Each input maps to a feature vector of shape $$n\times m$$

Then we can construct our Naive Bayes model for digit recognition,

$$
P(Y\|F_{0,0},\dots F_{n,m})\propto P(Y)\prod_{i,j}P(F_{i,j}\|Y)
$$

However, we have a problem now. We don’t know the probabilities, both prior and the likelihood. Therefore, we need to obtain the probability from the given dataset.

### Maximum Likelihood Estimation (MLE)

Note that our feature is binary valued. Recall the coin toss problem. We solved MLE problem to find the probability of coin showing head.

$$
\begin{align*}
\hat{p}&= \arg\max_p\log P(\mathcal{D}\|p) \\&= \arg\max_p\log\binom{\alpha_H+\alpha_T}{\alpha_H}p^{\alpha_H}(1-p)^{\alpha_T}\\
&= \frac{\alpha_H}{\alpha_H+\alpha_T}= \frac{k}{n}
\end{align*}
$$

Similarly, we wil count the number of the examples, denoted by $$Count(A=a,B=b)$$

First, compute the prior $$P(Y)$$. $$\pi$$ denotes the total number of examples.

$$
P(Y=y)=\frac{Count(Y=y)}{\sum_{y'}Count(Y=y')} = P(Y=y\|\pi)
$$

Also, the likelihood can be computed similarly,

$$
P(X_i=x\|Y=y) = \frac{Count(X_i=x, Y=y)}{\sum_{x'}Count(X_i=x', Y=y)} = P(X_i=x\|Y=y,\theta_i)
$$

### Training the Naive Bayes Model

Now we will train Naive Bayes model with given data for $$X$$ and $$Y$$.

For each value $$y_k$$, we will estimate the probability of class $$k$$,

$$
\pi_k \equiv P(Y=y_k)= \arg\max P(Y=y_k\|\pi_k)
$$

$$\pi_k$$ denotes the number of exmaples with class $$k$$.

Also, for each value $$x_{ij}$$ of each attribute $$X_i$$, we will estimate

$$
\theta_{ijk}\equiv P(X_i=x_{ijk}\|Y=y_k) = \arg\max P(X_i=x_{ijk}\|Y=y_k, \theta_{ijk})
$$

Then, we classify the the attributes $$X^{test}$$ by

$$
\hat{Y} = \arg\max_{y_k} P(Y=y_k)\prod_iP(X_i^{test}\|Y=y_k) = \arg\max_{y_k}\pi_k\prod_i\theta_{ijk}
$$

By applying MLE, we have

$$
\hat{\pi}_k= \hat{P}(Y=y_k) =\frac{\#D\{Y=y_k\}}{\|D\|}
$$

$$
\hat{\theta}_{ijk}=\hat{P}(X_i=x_{ij}\|Y=y_k) = \frac{\#D\{X_i=x_{ij}\cap Y=y_k\}}{\#D\{Y=y_k\}}
$$

Suppose we have 100 images as a dataset. There are 10 images per each digit.
Then, $$P(Y=y_k)=0.1$$ for all $$k$$. Therefore, $$\hat{\pi}_k =0.1$$ for all $$k$$. Also, $$\hat{\theta}_{ijk}$$ is the probability of the grid $$(i,j)$$ is on for each class $$k$$. Suppose you are looking at the grid $$(0,0)$$, which is on. If 2 of 10 images of class $$1$$ have the grid $$(0,0)$$ turned on, then $$\hat{\theta}_{001}=0.2$$.

With this process, we have obtained all the probabilities we need!
