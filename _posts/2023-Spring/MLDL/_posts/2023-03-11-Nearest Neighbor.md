---
layout: post
title: Nearest Neighbor
tags: [MLDL]
permalink: /2023-spring/mldl/nearest-neighbor
---

# Nearest Neighbor

# K-Nearest Neighbor (KNN)

- Uses a nearest neighbor as an inductive bias
  - Assign a label by majority of its neighbor’s labels
  - By doing so, it ignores outliers or exceptions → more generialzed
- Uses lazy learning
  - Learn by just storing a data
  - Predict by comparing a new data to the stored data
  - ↔ Eager learning (decision trees)
    - Learn by making an abstract model (useful pattern) from data
    - Predict by applying learned model to new data

## Distance Metrics

- Classification by nearby samples
- A exact notion of near is defined by the distance metrics
  - $$p=2:$$ L2 distance (Euclidean) : $$d(a,b)=\sqrt{\sum_{d=1}^D(a_d-b_d)^2 }$$
  - $$p=1$$ : L1 distance (Manhattan) : $$d(a,b)=\sum_{d=1}^D\|a_d-b_d\|$$
  - $$p=\infty$$ : Max norm (Chebyshev) : $$d(a,b)=\max(a_d - b_d)$$ (maximum component of $$\|a_d-b_d\|$$)
- Feature must be scaled
  - 10.1cm ↔ 10cm and 1.1cm ↔ 1cm both have 0.1cm difference, but the significance of the difference is different

## Hyperparameters

- We need to choose hyperparameter $$k$$
- $$k$$ refers the number of nearest neighbors
  - For example, if $$k=3$$, then one’s label is determined by the label of nearest 3 neighbors
  - if $$k= 1$$, one’s label is the same with the nearest neighbor (Voronoi diagram)
- $$k$$ tunes the complexity of the hypothesis space
  - Same as before,
    - higher $$k$$ will make smoother boundaries, but will be biased
    - lower $$k$$ will make complexed boundaries and will be overfitted
- Therefore, we need to choose better $$k$$ and these are practical ways
  - Cross-validation
  - Root of N
  - Odd number for $$k$$ (to avoid half-and-half case)

# VC Dimension

- A decision boundary of a classifier is the line that seperates positive and negative regions in the feature space
- It visualizes the complexity of the learned model
- To measure complexity of a model quantitavely, we introduce VC dimension
- VS is maximum number of points that can be arranged so that it shatters them → number of points that can be classified exactly
- A learning model can be expressed as $$f(x,w,b) = \text{sign}(x^Tw + b)$$

## Shattering

- Machine $$f$$ can shatter a set of points $$(x_1,\dots,x_r)$$
  ↔ For every possible training set of $$\exist$$, $$\exist \alpha \neq0$$ that gets zero training error (= classifies exactly for all possible data) - Each of $$y_1, \dots y_r$$ can be $$+1$$ or $$-1$$, so $$2^r$$ training sets should be considered
- A circle $$f(x,b)=\text{sign}(x^Tx -b)$$ has a VC dimension of 1
  ![cannot shatter points with opposite sign](Nearest%20Neighbor%20179bb48547184f56b4ee4b4bb8aba07e/Untitled.png)
  cannot shatter points with opposite sign
- A circle $$f(x,q, b)=\text{sign}(qx^Tx -b)$$ has a VC dimension of 2
  ![by adjusting signs of $$q, b$$, can shatter two points of opposite sign (if $$q,b <0$$, then area inside the circle is positive)](Nearest%20Neighbor%20179bb48547184f56b4ee4b4bb8aba07e/Untitled%201.png)
  by adjusting signs of $$q, b$$, can shatter two points of opposite sign (if $$q,b <0$$, then area inside the circle is positive)
- A line $$f(x,w,b)=\text{sign}(w^Tx+b)$$ has a VC dimension of 3
  - We can always draw six lines between four points
    - If 3 or 4 points are aligned, then we can rearrange until they aren not aligned
  - Then, two of those lines will cross
  - Therefore, a line can separate 3 points but not 4 → VC dim = 3
- The definition does not say that any set of n points can be shattered by the classifier
  - If there exists a set, and if it is the largest set, then number of it is the VC dimension

## Examples of VC-dimension

- Linear classifier
  - $$h = d+1$$ for $$d$$ dimensional feature
- Neural network
  - $$h = \text{\# of parameters}$$
- 1-nearest neighbor
  - $$h = \infty$$, as it can always classify exactly

# Curse of Dimensionality

- High dimension causes problems
  - As data become sparse, some algorithms become meaningless
  - Complexity of algorithms depending on the dimensionality become higher and therefore the algorithms become infeasible
  - Higher chance for two points to have same distance as dimensionality increases
    - There are much more possible two points that are in the specific distance
