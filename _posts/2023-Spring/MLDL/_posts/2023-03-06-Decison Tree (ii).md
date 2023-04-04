---
layout: post
title: Decision Tree (ii)
tags: [MLDL]
permalink: /2023-spring/mldl/decision-tree-2
---

# Decison Tree (ii)

# When to Stop Splitting

## Intuitive Idea

- There are some intuitive ideas for the base case
  1. Don’t split a node if all examples have the same label (entropy = 0)
  2. Don’t split a node if no attribute that can distinguish the examples
     - Case when every attribute is the same, but label is different
  3. ~~Don’t split if all attributes have zero information gain~~
     - It is different from the case 2
     - However, it isn’t good for splitting
     - Instead, perform pruning (undo) after building a tree
- With those ideas, we can make a simple algorithm for building a tree

![Untitled](<Decison%20Tree%20(ii)%20ccb823888bf14677aca41e7ffd701837/Untitled.png>)

- However, the tree gives large error for test set due to overfitting
- Therefore, we will introduce induction and regularization

## Induction and Regularization

- Regularizer → Inductive Bias (assumption)
  - For decision tree, we will _minimum description length_ for the inductive bias
- Our previous model was not generalized and lead to ovefitting
- Bias-Variance tradeoff
  - Simple model will give a biased solution (underfit)
  - Complex model will give a high-variance solution (overfit)
  - Therefore, we need to choose the best model between them
- Decision trees with no inductive bias will
  - have zero training set error (split until pure group)
  - have infinite variance
  - → must introduce some bias to make it simpler tree
    - e.g. fixed depth, fixed number of leaves, …

# Building Smaller Tree

- We will use short hypotheses as an inductive bias
- There are two possible approaches
  - Optimize on the held-out (validation) set
    - If growing the tree lowers the performance, then stop
    - It requires more data
  - Use statistical significance (Chi-square) testing
    - Stop if the test shows that any split is likely due to noises (i.e., difference is not significant and important)
    - It requres no additional data

## Chi-Square Test

- Chi-square tests whether split is statistically significant

- Let’s start with example
  - Proportion of data going to the left child
    $$p_L = 5/9$$
  - If data is randomly distributed, that is, each child has the same distribution, except for the size, it is expected that
    $$N_{AL}' = N_A\times p_L=10/9$$
    $$N'_{BL}=N_B\times p_L=35/9$$

![Untitled](<Decison%20Tree%20(ii)%20ccb823888bf14677aca41e7ffd701837/Untitled%201.png>)

- If a split is statistically significant, actual $$N_A$$ and $$N_B$$ must be sufficiently different from $$N_{AL}'$$ and $$N_{BL}'$$
  - if they are similar to each other, it means that the split cannot distinguish well → similar to randomly splitting
- Now we need to measure how much are they different
- The statistical significance can be measured with chi-square test
  - $$\chi^2$$ measures how much the split deviates from what we would get if the data is randomly splitted
  - Large $$\chi^2$$ means that the increase in $$IG$$ is significant
  - In this example, $$\chi^2=\frac{(1/9)^2}{10/9} + \frac{(-1/9)^2}{35/9} = 0.0321$$, which is very small, so we prune the split
- Formally, chi-square test is defined
  $$
  \chi^2 = \sum_{i,j} \frac{(N_{ij}-N_{ij}')^2}{N'_{ij}}
  $$
  - $$N_{ij}$$ = number of examples from class $$i$$ to child $$j$$
  - $$N'_{ij}=$$ number of examples from class $$i$$ to child $$j$$ assuming random selection
  - $$N'_{ij} = N_i\times p_j = N_i \times \frac{N_j}{N}$$
- Now we need to make a decision whether $$\chi^2$$ is large enough or too small
- If p-value, $$P(x > \chi^2) < 0.05$$, then we consider $$\chi^2$$ is large enough
  - threshold of p-value can be adjusted but conventionally use 0.05
    ![Untitled](<Decison%20Tree%20(ii)%20ccb823888bf14677aca41e7ffd701837/Untitled%202.png>)
  - Graph of p-value is affected by the degree of freedom
  - degree of freedom is computed by
  $$
  DF= (\#classes - 1)\times(\#children - 1)
  $$
  - in this example, $$P(x>0.0321) =0.858 > 0.05$$, so we don’t split
  - Large $$\chi^2$$ → small P-value → $$IG$$ of the split is significant and meaningful

## Reducing the Tree

- Now, we know which split is more significant, by computing $$\chi^2$$ and therefore p-value of each split
- Let $$P_{max}$$ be the threshold of P-value
- First, build the full standard decision tree (what we did before)
- From the bottom of the tree, prune the split if $$P_{chance}>P_{max}$$
  - $$P_{chance} > P_{max}$$ means that it the split is more random than what we want
  - $$P_{max}$$ is specified by the user
    - A tree with higher $$P_{max}$$ is more likely to overfit
    - A tree with smaller $$P_{max}$$ is more likely to be biased
- Continue to prune until no more node can be pruned
- For continuous attribute, we need to find some threshold that can convert to the binary tree
  - Choosing one branch for each integer will make tree overfit
  - We will split into $$X(x<t)$$ and $$X(x\ge t)$$ for some $$t$$ (threshold)
  - We choose threshold $$t$$ that gives the most $$IG$$

## Further Applications

- However, the accuracy of the decision tree is not so strong
- So we make more improvements
  - Random Forest → using set of trees
  - Boosting Trees
  - …
