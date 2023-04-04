---
layout: post
title: Decision Tree (i)
tags: [MLDL]
permalink: /2023-spring/mldl/decision-tree-1
---

# Decision Tree (i)

# Decision Tree

## Definition

A decision tool that uses a tree-like model of decisions and their possible consequences

For decision trees, we will use an fuel efficiency predicting tree as an example.

![Untitled](<Decision%20Tree%20(i)%209d29f0ee043049a1826af882e08ee40d/Untitled.png>)

- $$X$$ : attributes, $$Y$$: label, $$f$$: mapping function
- We will start with finding a hypothesis for $$f:X\rightarrow Y$$

## Hypotheses

- There are many possible representations for hypothesis
- It is natural to choose conjunction of attribute constraints
  - e.g. $$\text{maker = asia} \; \wedge \; \text{weight = low}$$
- An example is consistent with hypothesis, if the example logically satisfies the hypothesis
  - Let $$a= \text{asia} \;\|\; 5 \;\|\; \text{low} \;\|\; \text{low} \;\|\; \text{low}$$, then $$a$$ is consistent
  - But $$b= \text{usa} \;\|\; 4 \;\|\; \text{low} \;\|\; \text{low} \;\|\; \text{low}$$, is not consistent $$(\because \text{usa})$$
- A decision tree can represent any boolean function, but it requires too much nodes
  - For example, if there are 4 attributes, there are $$2^4=16$$ cases
  - For each case, label can be true or false, thus $$2^{16}$$ hypotheses are possible
  - Therefore, we need a better method
- By using conjunction of attribute of given data set, we can reduce the hypotheses
  - If there are $$2^4$$ conjunctive boolean functions
  - Now, we need to choose best one from it
  - Count the number of counterexamples for each boolean function, then choose one with the least counterexamples
  - However, it is not very good, so we will try better method

# Building a Tree

![(a)](<Decision%20Tree%20(i)%209d29f0ee043049a1826af882e08ee40d/Untitled%201.png>)

(a)

![(b)](<Decision%20Tree%20(i)%209d29f0ee043049a1826af882e08ee40d/Untitled%202.png>)

(b)

![(c)](<Decision%20Tree%20(i)%209d29f0ee043049a1826af882e08ee40d/Untitled%203.png>)

(c)

- Intuitively, we know that **(a)** is the best decision stump
- However, it is not easy to say which one of **(b)** or **(c)** is better
- So we will look over how to make a _good split_

## Recursive Split

- Our basic rule is based on a greedy heuristic
  - First, start from an empty tree
  - Then, split on next best attribute
  - Recurse (i.e. split again for each leaf node)
- Then, here comes two questions
  - What defines the **best** attribute?
  - In what condition the recursion ends? (i.e. what is the base case?)

## Measuring Uncertainty: Entropy

- To answer the first question, an uncertainty is introduced
- A split can be regarded good, if it makes classification very certain
  - If it is deterministic (i.e., all true or all false), then it is the best case
  - If it is uniform distribution, then it is the worst case
  - However, we are interested in the distribution in between them, which cannot be intuitively determined
- To measure uncertainty of those distributions in between, we introduce entropy.
- An entropy is the level of impurity in a group of examples
  - The more examples are mixed, the more uncertainty, and the higher entropy
  - Formally, an entropy of a random variable $$Y$$ is defined
    $$
    H(Y) = -\sum_{i=1}^kP(Y=y_i)\log_2P(Y=y_i)
    $$
  - For example, assume we have $$Y$$ such that $$P(Y=t)=\frac{5}{6}$$ and $$P(Y=f)=\frac{1}{6}$$
    - Then, $$H(Y)=-\frac{5}{6}\log_2\frac{5}{6} -\frac{1}{6}\log_2\frac{1}{6} = 0.65$$
- If entropy is low, the node is good for splitting, but not a good training set for learning
- Reversely, if entropy is high, it is not good for splitting, but is is good for training

## Conditional Entropy

![Untitled](<Decision%20Tree%20(i)%209d29f0ee043049a1826af882e08ee40d/Untitled%204.png>)

- Conditional entropy $$H(Y\|X)$$ of a random variable $$Y$$ conditioned on a random variable $$X$$ is defined by

$$
\begin{align*}
H(Y\|X) &= \sum_{x\in\Chi}P(X=x)H(Y\|X=x)\\
&= \sum_{x\in\Chi}P(X=x)(\sum_{y\in \Upsilon}-P(Y=y\|X=x)\log_2P(Y=y\|X=x))\\
&= -\sum_{x\in\Chi}P(X=x)\sum_{y\in\Upsilon}P(Y=y\|X=x)\log_2P(Y=y\|X=x)\\
&= \cdots\\
&= H(X, Y) - H(X)
\end{align*}
$$

- Conditional entropy indicates whether $$X$$ is helpful to predict $$Y$$

- For example, our $$X$$ and $$Y$$ are given
  - $$P(X_1=t)=\frac{4}{6}$$
  - $$P(X_2=f)=\frac{2}{6}$$
    ![Tree made from truth table on the right](<Decision%20Tree%20(i)%209d29f0ee043049a1826af882e08ee40d/Untitled%205.png>)
    Tree made from truth table on the right

![Truth table for $$X_1$$  and $$X_2$$](<Decision%20Tree%20(i)%209d29f0ee043049a1826af882e08ee40d/Untitled%206.png>)

Truth table for $$X_1$$ and $$X_2$$

$$
\begin{align*}H(Y\|X_1) &= -P(X_1=t)(P(Y=t\|X_1=t)\log_2P(Y=t\|X_1=t)\\ &+ P(Y=f\|X_1=t)\log_2P(Y=f\|X_1=t))\\ &- P(X_1=f)(P(Y=t\|X_1=f)\log_2P(Y=t\|X_1=f)\\ &+ P(Y=f\|X_1=f)\log_2P(Y=f\|X_1=f))\\ &= -\frac{4}{6}(1\log_21 +0\log_20)-\frac{2}{6}(\frac{1}{2}\log_2\frac{1}{2} + \frac{1}{2}\log_2\frac{1}{2})\\ &= \boxed{\frac{1}{3}}\end{align*}
$$

## Information Gain

- Information gain indicates how much entropy(or uncertainty) decreases by an attribute
- Formally, information gain by an attribute $$X_n$$ is defined

$$
IG(X_n)=H(Y) -H(Y\|X_1)
$$

- According to Jensen’s inequality, $$H(Y) \ge H(Y\|X_1)$$, thus $$IG(X_n)\ge 0$$
- Example
  - Lets recap the truth table above
  - We have $$H(Y) = 0.65$$ , $$H(Y\|X_1) =0.33,\ H(Y\|X_2)=0.46$$
  - Then information gain from each attributes are computed as
    - $$IG(X_1) = H(Y)-H(Y\|X_1)=0.65-0.33=0.32$$
    - $$IG(X_2)= H(Y)-H(Y\|X_2)=0.65-0.46=0.19$$
  - Then, $$IG(X_1)>IG(X_2)$$ means that splitting by $$X_1$$ gives more information, which is better
- It can be also regarded as $$Entropy_{parent} - \text{avg}(Entropy_{children})$$
  - For example, lets split $$Y$$ with attribute $$X_1$$
    - $$H(Y\|X_1=t) = -(1\log1+0\log0) = 0$$
    - $$H(Y\|X_1=f) = -(\frac{1}{2}\log\frac{1}{2}+\frac{1}{2}\log\frac{1}{2}) = 1$$
      - $$H(Y\|X_1=t)$$ $$H(Y\|X_2=t)$$ and $$H(Y\|X_1=f)$$ refer to the entropy of each child after making a split with $$X_1$$
    - But, $$X_1(x=t)$$ has 4 examples and $$X_1(x=f)$$ has 2 examples
    - Therefore, calculated weighted average of entropy of children
    - $$H(Y\|X_1) = H(Y) -(\frac{4}{6}\times  +\frac{2}{6}\times 1) = 0.65 - 0.33 = 0.32$$
    - It is consistent with former computation

# Better Decision Tree

- With information gain, now we know which attribute is most useful for discriminating between the classses
- When we split, compute the $$IG(X_n)$$ for each attribute and choose $$X_i^*$$, that gives the most information gain
  - For continuous attribute, set a threshold so that it behaves like a binary attribute
- Recursively execute the process, formally,

$$
\arg\max_iIG(X_i)=\arg\max_i(H(Y)-H(Y\|X_i)
$$

## Problems with Information Gain

- Splitting recursively with information gain will be executed until it cannot be splitted
- Then, it would split the data into pure but small subsets
- The tree will work well for training data, but won’t work for new data
  - Overfitting
- To solve this problem, we will discuss about the second question, _what would be the base case?_
