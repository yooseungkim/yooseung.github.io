---
layout: post
title: Naive Bayes Classifier (ii)
tags: [MLDL]
permalink: /2023-spring/mldl/naive-bayes-2
---

# Naïve Bayse Classifier (ii)

# Subtlety of Naïve Bayse

## Violating the Assumption

In fact, conditional independence is pretty strict assumption. Usually, features are not conditionally independent, so it violates the Naïve assumption.

But still, NB performs well eventhough the assumption is violated. It is because the actual probabilities $$P(Y\|X)$$ are often biased to 0 or 1. As we use binary classification, it often classifies well (since it does not require the posterior $$P(y_j\|x)$$ to be correct, but which $$y_j$$ makes it maximum)

## Overfitting

For MLE, we need to solve the optimization problem

$$
\arg\max_{y_k} P(Y=y_k)\prod_i P(X=x_i\|Y=y_k)
$$

But if there is no example with $$X = x_i$$ when $$Y= y_k$$, then MLE estimate $$P(X=x_i\|Y=y_k) = 0$$, therefore it cannot predict well.

Since it is hard to get more data, we need another way. To avoid the MLE estimate become zero, we will add “imaginary” examples for each cases.

Recall MAP and beta-distribution, we have the beta prior,

$$
\hat{p} = \frac{\alpha_H + \beta_H - 1}{\alpha_H+\beta_H + \alpha_T + \beta_T - 2}
$$

Now we will use MAP estimate on our dataset.

### Laplace Smoothing

Assume a beta-prior, which is equivalent to $$m$$ numbers of extra examples

$$
m = \sum_k \beta_k \text{ and } m_i = \sum_k\alpha_{i,k}
$$

$$\beta_k$$ is the number of examples with class $$k$$. And $$\alpha_{ik}$$ is the number of examples with $$X= x_i$$ and class $$k$$. From them, we have MAP estimate of

$$
\hat{\pi}_k = \hat{P}(Y=y_k) = \frac{\#D\{Y=y_k\} + \beta_k}{\|D\|+m}\\
\hat{\theta}_{ijk} = \hat{P}(X_i = x_{ij}\|Y=y_k) = \frac{\#D\{x_{ij} \wedge y_k\} + \alpha_{ik}}{\#D\{Y  = y_k\}+m_i'}
$$

If $$\alpha_{ik} =\beta_k \neq 0$$ for all $$i, k$$ , it is called **Laplace smoothing.** Now, even if we never observed a feature, the probability of posterior is never zero.

Therefore, the probability of $$X=x$$ after Laplace smoothing is

$$
P_{LAP,k} (x) = \frac{c(x) + k}{N + k\|X\|}
$$

For example, assume the example of coin toss with 2 heads and 1 tail. Then we have,

- $$P_{LAP, 0} (X) = \big<\frac{2}{3}, \frac{1}{3}\big>$$
- $$P_{LAP,1}(X) = \big<\frac{3}{5}, \frac{2}{5}\big>$$
- $$P_{LAP,100}(X) = \big<\frac{102}{203}, \frac{101}{203}\big>$$

Also, we can use Laplace smoothing for conditionals,

$$
P_{LAP, k}(x\|y) = \frac{c(x)+k}{c(y) + k\|X\|}
$$

# Text Classification

Now we will continue our discussion on the Naive Bayes classifier with text classification.

## Notation

Before going on, we need to clarify the notations.

First, $$Y$$is the whole set of documents, and $$Y=y$$ is the document with topic $$y$$.
And, $$X$$ is the entire document, and each $$X_i \in X=\{X_1, \dots, \}$$ is a $$i$$-th word of the document. Note that the domain of $$X_i$$ is the entire vocaulary, that is, $$X_i$$ can be any word.

We will classify the document as a topic $$\hat{y}$$ such that

$$
\begin{equation}
\hat{y}=h_{NB}(x) = \arg\max_yP(y) \prod_{i=1}^{Length}P(X_i\|y)
\end{equation}
$$

## Bag of Words

According to $$(1)$$, it can be easily observed that the position of a word matters. For example, the word “_love_” at 1st position and 10th position are distinguished.

But we make an additional naive assumption that the position in document does not matter. That is, the order of words on the page is ignored. Then our classification problem changes to

$$
\hat{y} = \arg\max _ y P(y)\prod_{i} P(w_i \| y)
$$

Therefore if $$X_i = X_j = w_k$$, then $$P(X_i\|y) = P(X_j\|y) = P(w_k\|y)$$. As we do not use the original document, instead, we use tokenized word distribution, we call this model “_bag of words_”.

## Learning and Testing

At learning phase, the model finds the probabilities, the prior $$P(Y)$$ and the likelihood $$P(w_i\|Y)$$
Prior $$P(Y)$$ is computed by counting how many documents from each topic. Also, the likelihood $$P(w_i\|Y)$$ is the fraction of times the $$w_i$$ appear among all words in all documents of $$y_j$$, which is computed by counting how many times you saw a word in a document of each topic. Due to our naive assumption, the model will ignore the order and share the distribution in all positions. Formally,

$$
P(y) = \frac{N_y}{N_{doc}}\\
P(w_i\|y_j) = \frac{count(w_i\|y_j)}{\sum_{w_k\in V} count(w_k\| y_j)}
$$

At the test phase, we will use naive Bayes decision rule for each document,

$$
h_{NB}(x) = \arg\max_y P(y)\prod_{i\in Position} P(w_i\|y)
$$

# Gaussian Naive Bayes

## Maximize the Likelihood Estimate

If the $$X_i$$ is continuous, we cannot use the preivious method. Therefore, we will use **Gaussian Naive Bayes**,

$$
P(X_i = x\|Y=y_k) = \frac{1}{\sigma_{ik}\sqrt{2\pi}}e^{\frac{-(x-\mu_{ik})^2}{2\sigma_{ik}^2}}
$$

If the variance is independent of $$Y$$, then $$\sigma_{ik} = \sigma_i$$. Or, if it is independent of $$X$$, then $$\sigma_{ik}=\sigma_k$$.

For each value $$y_k$$, we will estimate $$\pi_k = P(Y=y_k)$$ and for each $$X_i$$, estimate class conditional mean $$\mu_{ik}$$ and variance $$\sigma_{ik}$$. Therefore, we will classify $$X^{test}$$ with

$$
\hat{Y} = \arg\max_{y_k} P(Y=y_k)\prod_{i}P(X_i^{test}\|Y=y_k)\\
= \arg\max_{y_k}\pi_k\prod_{i}N(X_i^{test};\mu_{ik}, \sigma_{ik})
$$

It is finding the class with the largest posterior, which means that it is most probable to be class of $$y_k$$. Also note that $$Y$$ is discrete, not continuous.

By using MLE, we can estimate the parameter $$\mu_{ik}$$ and $$\sigma_{ik}$$,

$$
\hat{\mu}_{ik} = \frac{1}{\sum_j\delta(Y^j=y_k)} \sum_jX_i^j\delta(Y^j=y_k)\\
\hat{\sigma}_{ik} = \frac{1}{\sum_j\delta(Y^j=y_k) - 1}\sum_j (X_i^j-\hat{\mu}_{ik})^2 \delta(Y^j=y_k)
$$

As $$\delta(Y^j=y_k) = 1$$ only if $$Y^j =y_k$$, the expression $$\sum_j\delta(Y^j=y_k)$$ is the number of $$y_k$$’s.

Similarly, $$\sum_jX_i^j\delta(Y^j=y_k)$$ is sum of $$X_i$$’s, whose class is labelled with $$y_k$$.
($$i,j,k$$ refers to _feature, example,_ and _class,_ respectively)

## Geometrical View

Let’s consider an example, classifying males and females based on height and weight. Then the classifier is given by

$$
\hat{f}(x)= \argmax_{y \in \{male, female\}} P(X=x_i\|Y=y)\cdot P(Y=y)
$$

The model will learn class prior by

$$
P(Y=male) = \frac{\# males}{N},\;\;\; P(Y=female)=\frac{\#females}{N}
$$

Also, the class conditionals will be learned by m

$$
P(X\|Y=male) = p_{\theta(male)}(X) \;\;\text{: MLE using only male data}\\
P(X\|Y=female) = p_{\theta(female)}(X)\;\; \text{: MLE using only female data}
$$

This classification can be represented with a graph with decision boudaries.

![The yellow line is the decision boundary of the Gaussian Naive Bayes (not linear)](<Nai%CC%88ve%20Bayse%20Classifier%20(ii)%20b66b25dd957e4ef99c00d6d754350666/Untitled.png>)

The yellow line is the decision boundary of the Gaussian Naive Bayes (not linear)

And Naive Bayes is a linear classifier under some conditions, as shown below

![Untitled](<Nai%CC%88ve%20Bayse%20Classifier%20(ii)%20b66b25dd957e4ef99c00d6d754350666/Untitled%201.png>)

Also, if the features are continuous, i.e., using Gaussian Naive Bayes, we can show that

$$
P(y\|\mathbf{x})=\frac{1}{1+e^{-y(\mathbf{w}^T\mathbf{x}+b)}}
$$

Therefore, we can use logistic regression in this case.
